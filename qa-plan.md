# FRAMEWAR — QA Plan

**Project**: FRAMEWAR (Animation Studio Simulation)
**QA Lead**: CRASH
**Version**: 1.0
**Date**: 2026-02-07
**Status**: Pre-Production QA Framework

---

## 1. WHAT WE'RE TESTING (AND WHAT COULD GO WRONG)

This is a management sim where players shepherd animated films through 3-4 year production cycles. The entire game is a simulation running on invisible math. No physics. No real-time combat. No player reflexes. That means every bug is a systems bug — a cascade of bad data, broken logic, or edge cases nobody thought to test.

Here's what kills sims: the player makes 500 decisions over 10 hours, and decision #247 breaks the economy in a way that doesn't surface until decision #380. By then, the save is corrupted and the player has no idea what went wrong. They just know the game is broken.

**What could make this unfun:**

1. **Film DNA scores feel random.** Player invests in story, gets low STORY DEPTH, has no idea why. The entire creative fantasy collapses if causality is opaque.
2. **Economy breaks.** Budget goes negative infinity. Or positive infinity. Player is either bankrupt by Year 3 or so rich by Year 5 that all tension evaporates.
3. **Decisions don't matter.** All films score 6.5-7.5 regardless of player choices. Optimization is impossible because there's nothing to optimize.
4. **Save/load desync.** Load a save, advance one quarter, save again. The two files differ. Simulation is non-deterministic. Player loses trust.
5. **UI lies.** Production board says "3 quarters remaining," but film never completes. Budget display says "$120M," but the player is actually bankrupt. The presentation layer is out of sync with simulation state.
6. **Rival AI is wallpaper.** Rivals never compete, never poach talent, never matter. The "war" in FRAMEWAR is cosmetic.
7. **Late-game performance death spiral.** Quarter 50, three active films, 60 staff members, quarterly tick takes 15 seconds. Game becomes unplayable.
8. **Procedural content is garbage.** Film concepts are Mad Libs nonsense. Reviews read like a Markov chain. The player stops caring because the content has no authorial voice.

Every test in this plan addresses one of these failure modes. If we catch them all, the game ships. If we miss one, we read about it in 1-star Steam reviews.

---

## 2. TEST PLAN STRUCTURE

### 2.1 Test Phases

**PHASE 1: UNIT & INTEGRATION (Months 1-6)**
- Validate individual systems in isolation.
- Verify Film DNA scoring, box office formulas, tech tree unlocks, talent management calculations.
- All tests automated where possible.

**PHASE 2: VERTICAL SLICE VALIDATION (Months 4-6)**
- Full playthrough of 3-film campaign (1995-2003).
- Validate core loop is fun, legible, and bug-free.
- Decision attribution is clear.

**PHASE 3: FULL CAMPAIGN TESTING (Months 7-10)**
- 60-quarter playthroughs with varied strategies.
- Edge case discovery: all-2D studio, sequel-only studio, bankruptcy recovery, AI competition.
- Performance profiling at scale.

**PHASE 4: REGRESSION & POLISH (Months 11-12)**
- Automated regression suite runs nightly.
- Platform-specific testing (PC, Switch, iPad).
- Save/load stress tests.
- Content quality pass (review all 100 film concepts, 25 review templates).

**PHASE 5: CERTIFICATION & RELEASE (Month 13+)**
- Steam pre-release QA.
- Switch lotcheck prep (if applicable).
- Day-one patch readiness.

### 2.2 Test Ownership

- **Programmer (BYTE)**: Automated unit tests, determinism validation, performance profiling.
- **Designer (REED)**: Balance testing, formula verification, content quality.
- **QA Lead (CRASH, me)**: Full-playthrough testing, edge case hunting, regression management, bug triage.
- **Contract QA (Months 11-12)**: Platform-specific testing, certification compliance.

---

## 3. CORE SYSTEMS TEST CASES

### 3.1 Film Production Pipeline

**What we're validating:** A film moves through six phases (Development → Pre-Production → Production → Post-Production → Marketing → Release). Each phase modifies Film DNA scores. The player's decisions during phase gates determine outcomes.

#### Test Case 3.1.1: Basic Pipeline Progression
**Preconditions:**
- Fresh campaign start (Q1 1995).
- Greenlight one film: $60M budget, CG approach, 3-year target.
- Assign Director (VISION 7, EGO 5).

**Steps:**
1. Advance quarters until Development phase completes (should be 2-3 quarters).
2. Verify phase gate decision prompt appears.
3. Choose story outline option A (favors HEART over HUMOR).
4. Advance quarters until Pre-Production completes (2-3 quarters).
5. Verify STORY DEPTH base score is set (check Film details screen).
6. Continue through Production, Post, Marketing phases.
7. Film releases at target quarter.

**Expected Results:**
- Film progresses through all 6 phases without stalling.
- Each phase gate decision prompt appears exactly once.
- Phase durations match config (Development 2-3Q, PreProd 2-3Q, Production 3-5Q, etc.).
- Film DNA scores are locked at correct phase boundaries (STORY DEPTH after Dev, VOICE CAST APPEAL after PreProd, ANIMATION QUALITY after Prod).
- Film status displayed correctly on production board at all times.

**Severity if fails:** CRITICAL. Core loop is broken.

#### Test Case 3.1.2: DNA Score Attribution
**Preconditions:**
- Film in Development phase.

**Steps:**
1. Select story outline that grants STORY DEPTH +0.5.
2. Invest extended Development time (+1 quarter).
3. Phase completes. Check STORY DEPTH score.
4. Open post-mortem screen (or decision history viewer).
5. Verify attribution shows:
   - Story Artist base contribution.
   - Director VISION bonus.
   - Extended development bonus.
   - Story outline choice modifier.

**Expected Results:**
- STORY DEPTH = Story Artist skill + Director bonus + time bonus + outline modifier.
- Attribution breakdown matches calculation exactly.
- No "mystery points" — every 0.1 of score is explained.

**Severity if fails:** HIGH. Opaque scoring kills creative stewardship fantasy.

#### Test Case 3.1.3: Phase Gate Decision Consequences
**Preconditions:**
- Film in Pre-Production phase.
- Director requests storyboard revision (costs +1 quarter, +$3M, grants STORY DEPTH +0.5).

**Steps:**
1. Approve revision.
2. Verify:
   - Film.QuartersInCurrentPhase resets to 0.
   - Budget decreases by $3M.
   - Decision logged in DecisionHistory.
3. Complete phase. Verify STORY DEPTH includes +0.5 modifier.

**Expected Results:**
- Approving revision extends phase by 1 quarter.
- Budget deducted immediately.
- STORY DEPTH reflects decision when phase completes.

**Severity if fails:** HIGH. Decisions must have visible, legible consequences.

#### Test Case 3.1.4: Hidden Risk Reveal
**Preconditions:**
- Greenlight film with hidden risk "Third Act Problem" (caps STORY DEPTH at 7 unless addressed).

**Steps:**
1. Advance to Development phase gate.
2. Verify risk is revealed in decision prompt.
3. Option A: Address risk (costs +1Q, +$5M, removes cap).
4. Option B: Ignore risk (no cost, cap remains).
5. Test both paths. Verify STORY DEPTH cap applies or doesn't based on choice.

**Expected Results:**
- Risk revealed at correct phase (Development for "Third Act Problem").
- If addressed: no STORY DEPTH cap, costs applied.
- If ignored: STORY DEPTH cannot exceed 7 regardless of other modifiers.

**Severity if fails:** MEDIUM. Hidden risks must matter or they're noise.

#### Test Case 3.1.5: Multi-Film Production Collision
**Preconditions:**
- Two films in Production phase simultaneously.
- Render farm capacity = 100%.
- Film A allocated 60%, Film B allocated 50% (total 110% = over capacity).

**Steps:**
1. Verify system flags over-allocation.
2. Player must reduce allocation or risk render farm crisis event.
3. Trigger crisis: keep over-allocation for 2 quarters.
4. Verify crisis event: hardware failure, lose 1 quarter render progress on one film.

**Expected Results:**
- Over-allocation warnings appear in UI.
- Crisis event triggers at expected threshold.
- Film Production phase extended by 1 quarter as penalty.

**Severity if fails:** MEDIUM. Resource contention is a key strategic layer.

### 3.2 Film DNA System

**What we're validating:** Every film has 8 DNA scores (STORY DEPTH, ANIMATION QUALITY, HUMOR, HEART, SPECTACLE, VOICE CAST APPEAL, ORIGINALITY, REWATCHABILITY) determined by player decisions. Scores feed into box office and review formulas. Scoring must be deterministic and legible.

#### Test Case 3.2.1: DNA Score Boundaries
**Preconditions:**
- Film with maximal inputs: best Story Artist (SKILL 10), best Director (VISION 10), full Development time, optimal tech tree.

**Steps:**
1. Make all "best case" decisions during production.
2. Verify STORY DEPTH does not exceed 10.0.
3. Verify ANIMATION QUALITY ceiling is respected (tech tree dependent).
4. Verify no DNA score goes below 0.0 even with worst decisions.

**Expected Results:**
- All DNA scores clamped to [0.0, 10.0] range.
- Ceilings enforced by tech tree (e.g., ANIMATION QUALITY capped at 7.0 if missing key CG nodes).

**Severity if fails:** MEDIUM. Score bounds prevent formula exploits.

#### Test Case 3.2.2: DNA Interaction Effects
**Preconditions:**
- Film with HEART = 8.0, STORY DEPTH = 8.0.

**Steps:**
1. Calculate critic score (Projector Score).
2. Verify formula applies HEART multiplier to STORY: `Effective Story = STORY DEPTH * (1 + HEART * 0.05)`.
3. Expected: 8.0 * (1 + 8.0 * 0.05) = 8.0 * 1.4 = 11.2 effective story for critics.
4. Repeat with HEART = 4.0. Verify weaker multiplier.

**Expected Results:**
- HEART boosts STORY DEPTH's weight in critic formula.
- Interaction is additive, not random.

**Severity if fails:** HIGH. Interaction effects are the strategic depth.

#### Test Case 3.2.3: ORIGINALITY Variance
**Preconditions:**
- Two films, both ORIGINALITY = 9.0, identical DNA otherwise.

**Steps:**
1. Release both films.
2. Check Projector Scores.
3. Verify variance: scores should differ by up to ±3 points due to high ORIGINALITY (per design).
4. Repeat with ORIGINALITY = 3.0 films. Verify variance is ±0.5 (low risk).

**Expected Results:**
- High ORIGINALITY = high critic score variance (risk/reward).
- Low ORIGINALITY = low variance (safe).

**Severity if fails:** MEDIUM. Variance must reward bold swings without being chaotic.

#### Test Case 3.2.4: VOICE CAST APPEAL Diminishing Returns
**Preconditions:**
- Film with VOICE CAST APPEAL = 7.0.
- Hire additional celebrity voice actor to push VOICE CAST APPEAL to 9.0.

**Steps:**
1. Calculate box office opening weekend before and after hire.
2. Verify: points above 7.0 contribute at 50% normal impact (per design doc).
3. Compare cost ($12M for celebrity) vs. revenue gain.

**Expected Results:**
- Pushing VOICE CAST from 7 to 9 yields diminishing returns.
- High celebrity spending is not always optimal.

**Severity if fails:** MEDIUM. Prevents "always hire biggest star" dominant strategy.

### 3.3 Box Office & Reviews System

**What we're validating:** Film releases trigger a 4-week box office simulation. Revenue calculated from Film DNA, awareness, competition, season. Reviews generated procedurally. Formulas must be deterministic, balanced, and generate plausible outcomes.

#### Test Case 3.3.1: Opening Weekend Formula Determinism
**Preconditions:**
- Film with known DNA scores, $80M budget, 70 AWARENESS, summer release, no competition.

**Steps:**
1. Calculate expected opening weekend manually using formula from tech doc:
   ```
   Base = (80M / 4) * (DNA composite / 7)
   Awareness Mult = 0.5 + (70 / 100) = 1.2
   Star Power = 1 + (highest actor star power * 0.03)
   Season = 1.3 (summer)
   Competition = 1.0 (none)
   ```
2. Release film. Verify opening weekend matches calculation ±1% (rounding tolerance).
3. Save before release, load, release again. Verify identical result (determinism).

**Expected Results:**
- Opening weekend revenue matches formula exactly.
- Reloading save produces identical outcome.

**Severity if fails:** CRITICAL. Non-deterministic box office breaks player trust.

#### Test Case 3.3.2: Drop-Off Rate (Legs vs. Frontload)
**Preconditions:**
- Film A: HEART 9, REWATCHABILITY 8, SPECTACLE 6, STORY DEPTH 8 (high legs).
- Film B: SPECTACLE 9, STORY DEPTH 4, HEART 5, REWATCHABILITY 5 (frontloaded).

**Steps:**
1. Release both films with identical opening weekends ($40M).
2. Track weekly drops.
3. Film A should have lower drop rate (high HEART/REWATCHABILITY reduce drop).
4. Film B should have higher drop rate (SPECTACLE > STORY increases drop).
5. By Week 4, Film A should have higher total gross despite same opening.

**Expected Results:**
- Film A total gross > Film B total gross (legs vs. frontload).
- Drop rate formula matches design doc.

**Severity if fails:** HIGH. Leg vs. frontload dynamic is key strategic distinction.

#### Test Case 3.3.3: Competition Effect
**Preconditions:**
- Player film releases Q2 2003.
- Rival film (same genre, high budget) also releases Q2 2003.

**Steps:**
1. Release player film.
2. Verify competition modifier applied (0.6-0.8x box office per design).
3. Check UI displays competing film and warns player.

**Expected Results:**
- Opening weekend reduced by 20-40% due to competition.
- UI clearly communicates competitive pressure.

**Severity if fails:** MEDIUM. Competition must be a real strategic factor.

#### Test Case 3.3.4: Projector Score Calculation
**Preconditions:**
- Film with DNA composite 7.5, ORIGINALITY 8, Director with track record avg 75.

**Steps:**
1. Calculate Projector Score manually:
   ```
   Base = 7.5 * 10 = 75
   Originality bonus = 8 * 2 = 16
   Director bonus = 75 * 0.15 = 11.25
   Era alignment = +5 (CG film in 2003)
   Variance = ±5
   Total = 75 + 16 + 11 + 5 + variance = 107 ± 5 → clamped to 100
   ```
2. Release film. Verify Projector Score is 95-100 (clamped).

**Expected Results:**
- Projector Score matches formula.
- Score clamped to [0, 100] range.

**Severity if fails:** MEDIUM. Critic scores must be legible and fair.

#### Test Case 3.3.5: Procedural Review Quality
**Preconditions:**
- Film with HEART 9, STORY 8, SPECTACLE 5.

**Steps:**
1. Release film. Generate 10 reviews.
2. Read reviews. Verify:
   - Reviews reference high HEART/STORY (e.g., "emotionally devastating," "profound storytelling").
   - Reviews don't praise SPECTACLE (it's middling).
   - No nonsensical phrases or broken grammar.
3. Repeat 5 times. Verify reviews vary (not identical each playthrough).

**Expected Results:**
- Reviews contextually match film's DNA profile.
- Phrases feel authored, not algorithmic.
- Variety across multiple releases.

**Severity if fails:** HIGH. Generic reviews kill immersion.

### 3.4 Talent Management System

**What we're validating:** Hire/fire Directors, Animators, Story Artists, Voice Actors. Morale degrades with crunch or overrides. Talent can be poached by rivals. Salary inflation tracked. Crunch has escalating costs.

#### Test Case 3.4.1: Talent Hiring & Assignment
**Preconditions:**
- Budget $80M. Hire Director ($2M fee), 6 Animators ($150K/year each).

**Steps:**
1. Verify budget decreases by $2M (Director) + $900K (Animators annual, prorated for quarters remaining in year).
2. Assign Director to Film A.
3. Assign 4 Animators to Film A, 2 to Film B.
4. Verify production phase resource allocations reflect assignments.

**Expected Results:**
- Hiring costs deducted correctly.
- Assigned talent locked to specific films.
- Cannot assign same person to two films simultaneously.

**Severity if fails:** MEDIUM. Talent logistics must be clear.

#### Test Case 3.4.2: Crunch Mechanics & Morale Decay
**Preconditions:**
- Film in Production. 4 Animators assigned (morale all at 80).

**Steps:**
1. Activate crunch for 1 quarter.
2. Verify:
   - Animator SPEED +2 for that quarter.
   - Animator morale -20 each.
   - Production phase completes faster (fewer quarters required).
3. Continue crunch for 3 consecutive quarters.
4. Verify:
   - Studio Culture Penalty triggered (event notification).
   - All studio morale -10.
   - Future hiring costs +20% for 1 year.
5. One animator morale drops below 30. Verify 15% quit chance per quarter.

**Expected Results:**
- Crunch boosts speed but degrades morale.
- Consecutive crunch triggers culture crisis.
- Quit threshold enforced.

**Severity if fails:** HIGH. Crunch must be a meaningful cost, not free speed.

#### Test Case 3.4.3: Talent Poaching by Rivals
**Preconditions:**
- Animator with morale 25 (low), salary $120K (below market $180K).
- Rival studio with aggressive poaching strategy.

**Steps:**
1. Advance quarter. Verify poaching attempt triggers (30% chance per design).
2. Player receives notification: "Luminos Animation is attempting to poach [Animator Name]."
3. Options: counter-offer (raise salary to $180K+), let them go.
4. Counter-offer. Verify animator stays, salary updated.
5. Reload save, choose "let them go." Verify animator removed from roster, appears in rival filmography later.

**Expected Results:**
- Poaching attempts occur at designed frequency.
- Player can counter-offer or accept loss.
- Poached talent visibly joins rival (not just deleted).

**Severity if fails:** MEDIUM. Talent wars must feel real.

#### Test Case 3.4.4: Director Morale & Loyalty
**Preconditions:**
- Director (VISION 8, EGO 7) assigned to film.
- Player overrides Director's creative vision 3 times during production.

**Steps:**
1. Each override: Director morale -15.
2. After 3 overrides, morale = 100 - 45 = 55.
3. Film wraps. Director loyalty check.
4. Rival studio offers better deal. Verify Director has 40% chance to leave (low morale).
5. If leaves, verify Director appears in rival's roster.

**Expected Results:**
- Overrides degrade Director morale visibly.
- Low morale increases departure risk.
- Lost Directors benefit rivals.

**Severity if fails:** MEDIUM. Creative tension must have stakes.

#### Test Case 3.4.5: Voice Actor Scheduling Conflicts
**Preconditions:**
- Voice Actor available only Q3-Q4 2002.
- Film in Pre-Production during Q1 2002.

**Steps:**
1. Attempt to cast Voice Actor.
2. Verify warning: "Actor not available until Q3."
3. Options: wait (delay Pre-Production by 2 quarters), cast alternate actor.
4. Test both paths. Verify delay extends phase if waiting.

**Expected Results:**
- Scheduling conflicts are enforced.
- Player can delay or pivot.

**Severity if fails:** LOW. Minor strategic layer, not core.

### 3.5 Technology Tree System

**What we're validating:** Research tech nodes. Nodes have prerequisites, costs, research time. Unlocked nodes boost Film DNA ceilings/floors. Retroactive application to in-progress films possible (with cost).

#### Test Case 3.5.1: Tech Unlock & Effects
**Preconditions:**
- Research "Subsurface Scattering" ($8M, 4 quarters).

**Steps:**
1. Initiate research. Verify budget -$8M, research timer starts.
2. Advance 3 quarters. Verify research not yet complete.
3. Advance 1 more quarter (total 4). Verify:
   - Research completes.
   - Tech unlocked (visible in tree, checkmark/green highlight).
   - ANIMATION QUALITY ceiling +1 for CG films.
4. Greenlight new CG film. Verify ANIMATION QUALITY ceiling reflects unlock.

**Expected Results:**
- Research time matches config.
- Cost deducted upfront.
- Effects applied globally to studio.

**Severity if fails:** MEDIUM. Tech tree must provide visible benefits.

#### Test Case 3.5.2: Prerequisite Enforcement
**Preconditions:**
- "Advanced Fur/Hair" requires "Basic Fur/Hair" (not yet unlocked).

**Steps:**
1. Attempt to research "Advanced Fur/Hair."
2. Verify: UI greys out node, tooltip shows "Requires: Basic Fur/Hair."
3. Research and unlock "Basic Fur/Hair."
4. Verify "Advanced Fur/Hair" becomes available.

**Expected Results:**
- Prerequisites strictly enforced.
- Dependency chain visible in UI.

**Severity if fails:** MEDIUM. Broken prerequisites create exploits.

#### Test Case 3.5.3: Retroactive Tech Application
**Preconditions:**
- Film in Production (Quarter 3 of 5).
- "Global Illumination" tech completes during Production.

**Steps:**
1. Tech completes. Notification: "Global Illumination unlocked. Apply to [Film Name]?"
2. Options: Apply (costs +$3M, +1 quarter delay), Ignore (affects next film only).
3. Apply. Verify:
   - Budget -$3M.
   - Film Production phase extended by 1 quarter.
   - ANIMATION QUALITY ceiling updated for this film.

**Expected Results:**
- Retroactive application is optional.
- Costs and delays applied correctly.

**Severity if fails:** MEDIUM. Timing strategy must work as designed.

#### Test Case 3.5.4: 2D vs. CG Branch Isolation
**Preconditions:**
- Unlocked "Stylized Rendering" (2D branch).
- Greenlight CG film.

**Steps:**
1. Verify "Stylized Rendering" effects do NOT apply to CG film.
2. Greenlight 2D film. Verify effects apply.

**Expected Results:**
- Tech branch benefits are technology-specific.
- No cross-contamination.

**Severity if fails:** LOW. Clear but not critical.

### 3.6 Economy System

**What we're validating:** Budget pool. Income from box office, home video, merchandise. Expenses: salaries, production budgets, R&D, marketing, overhead. Bankruptcy threshold. Cash flow across multi-year film production gaps.

#### Test Case 3.6.1: Quarterly Expense Calculation
**Preconditions:**
- Budget pool $100M.
- Active: Film A (Production, $5M/quarter burn), Film B (Development, $2M/quarter).
- Salaries: $1.5M/quarter.
- Overhead: $2M/quarter.
- R&D: $3M/quarter (active research).

**Steps:**
1. Advance quarter.
2. Verify budget = $100M - $5M - $2M - $1.5M - $2M - $3M = $86.5M.
3. Check UI displays updated budget.

**Expected Results:**
- All expense categories deducted correctly.
- Budget display matches calculated value.

**Severity if fails:** CRITICAL. Budget math errors cascade catastrophically.

#### Test Case 3.6.2: Revenue Flow & Timing
**Preconditions:**
- Film releases Q1 2003. Domestic gross $150M, international $220M.
- Studio share: 45% domestic + 35% international = $67.5M + $77M = $144.5M.

**Steps:**
1. Film releases. Verify budget increases by $144.5M (rounded to nearest $0.1M).
2. Home video revenue (40% of domestic = $60M) arrives Q3 2003 (2 quarters later).
3. Advance to Q3. Verify budget increases by $60M.

**Expected Results:**
- Theatrical revenue immediate.
- Home video delayed by 2 quarters.

**Severity if fails:** HIGH. Revenue timing affects cash flow strategy.

#### Test Case 3.6.3: Bankruptcy Threshold
**Preconditions:**
- Budget pool -$25M (in debt but above -$30M threshold).

**Steps:**
1. Advance quarter with $10M expenses. Budget = -$35M (below threshold).
2. Verify CRISIS MODE triggers:
   - Forced layoffs (player chooses 30% of staff to cut).
   - Forced production cancellation (player chooses 1 active film to cancel).
   - Emergency loan: +$40M, but -10% revenue split on next 2 releases.
3. After crisis, budget = -$35M + $40M = $5M.
4. Verify penalties apply to next releases.

**Expected Results:**
- Crisis triggers at -$30M.
- Player makes painful choices.
- Emergency loan has visible cost.

**Severity if fails:** CRITICAL. Bankruptcy must be survivable but punishing.

#### Test Case 3.6.4: Salary Inflation Over Time
**Preconditions:**
- Q1 1995: Top animator salary $200K. Top voice actor $3M.

**Steps:**
1. Advance to Q1 2000 (20 quarters).
2. Check market salaries. Verify:
   - Animator salary inflated ~3-5% per year → $230K-$250K.
   - Voice actor salary inflated ~5-10% per year → $4.8M-$7M.
3. Hire new talent. Verify costs match inflated rates.

**Expected Results:**
- Salaries increase over campaign.
- Inflation rates match design doc.

**Severity if fails:** MEDIUM. Inflation creates late-game economic pressure.

### 3.7 Rival Studio AI

**What we're validating:** 2-3 rival studios greenlight and release films. Rivals have strategies (Prestige, Commercial, Technical, Franchise). Rivals compete for box office, awards, talent. Rival behavior must be readable and credible.

#### Test Case 3.7.1: Rival Film Release & Competition
**Preconditions:**
- Player film releases Q2 2002 (summer, high SPECTACLE).
- Rival "Luminos Animation" releases Q2 2002 (prestige film, high STORY).

**Steps:**
1. Both films release same quarter.
2. Verify:
   - Player film box office reduced by competition modifier (20-40%).
   - Rival film displayed in "Competing Releases" section of player's box office screen.
   - UI warns player before release: "Luminos is releasing [Film Name] this quarter."
3. Check awards season. Both films eligible. Verify rival film competes in Oscar nominations.

**Expected Results:**
- Competition reduces player box office.
- Rival presence is visible and credible.
- Awards race includes rival films.

**Severity if fails:** HIGH. Rivals must feel like real competitors.

#### Test Case 3.7.2: Rival Strategy Consistency
**Preconditions:**
- Rival "TitanToon Animation" has COMMERCIAL strategy.

**Steps:**
1. Track TitanToon's releases over 10 years.
2. Verify:
   - Most films are high-SPECTACLE, high-AUDIENCE BREADTH.
   - Sequels are common (franchise focus).
   - Release timing favors summer/holiday (high box office seasons).
   - Low ORIGINALITY films (safe bets).

**Expected Results:**
- Rival strategy is consistent and readable.
- Player can predict rival behavior.

**Severity if fails:** MEDIUM. Rivals need distinct identities.

#### Test Case 3.7.3: Rival Talent Poaching
**Preconditions:**
- Player has lead Animator (QUALITY 9, morale 40, underpaid).
- Rival "Luminos" has TECHNICAL strategy (aggressive poaching).

**Steps:**
1. Advance quarter. Verify poaching attempt.
2. Player receives offer from Luminos: "They're offering $250K (you pay $180K)."
3. Player declines. Animator leaves. Check Luminos roster in rival studio UI.
4. Later, Luminos releases film with higher ANIMATION QUALITY (benefit from poached talent).

**Expected Results:**
- Poaching happens. Player sees consequences.
- Rival benefits from stolen talent.

**Severity if fails:** MEDIUM. Poaching must matter strategically.

#### Test Case 3.7.4: Rival AI "Dumb" Decisions (Humanizing)
**Preconditions:**
- Rival releases 4th sequel in franchise despite fatigue warnings.

**Steps:**
1. Track sequel performance. Verify diminishing returns (fatigue mechanic).
2. Rival's 4th sequel underperforms (low gross, low Projector Score).
3. Verify rival's reputation drops (COMMERCIAL takes a hit).

**Expected Results:**
- Rivals occasionally make suboptimal choices (like humans).
- Poor choices have consequences.

**Severity if fails:** LOW. Nice-to-have for immersion.

### 3.8 Procedural Content Systems

**What we're validating:** Film concepts generated from 100 templates. Reviews generated from 25 templates. Content must feel authored, not algorithmic. Variety across playthroughs. No nonsensical combinations.

#### Test Case 3.8.1: Film Concept Generation Quality
**Preconditions:**
- Studio with PRESTIGE reputation 75 (should receive high-ORIGINALITY concepts).

**Steps:**
1. Generate 20 film concepts at Greenlight Table.
2. Read loglines. Verify:
   - No broken grammar or placeholder text like "[PROTAGONIST]" (unfilled variables).
   - Concepts match studio reputation (high ORIGINALITY, 7-10 range).
   - Concepts vary (not all similar premises).
   - Loglines feel authored (could plausibly be pitched by a real person).
3. Repeat across 3 playthroughs. Verify different concepts appear.

**Expected Results:**
- Concepts are grammatically correct.
- Loglines feel creative and varied.
- Reputation influences concept quality.

**Severity if fails:** CRITICAL. Greenlight is the core fantasy. Bad concepts kill it.

#### Test Case 3.8.2: Review Generation Contextual Fit
**Preconditions:**
- Film A: SPECTACLE 9, STORY 4, HEART 3 (all flash, no substance).
- Film B: HEART 9, STORY 9, SPECTACLE 5 (quiet emotional depth).

**Steps:**
1. Release both films. Generate reviews.
2. Film A reviews should mention:
   - "Visually stunning," "dazzles the eyes," "hollow core," "forgettable story."
3. Film B reviews should mention:
   - "Emotionally devastating," "profound," "quietly powerful," "transcendent."
4. Verify reviews DO NOT praise Film A's story or Film B's spectacle.

**Expected Results:**
- Reviews contextually match film DNA profiles.
- No generic "it was good/bad" reviews.

**Severity if fails:** HIGH. Generic reviews break immersion.

#### Test Case 3.8.3: Procedural Content Edge Cases
**Preconditions:**
- Film with all DNA scores = 5.0 (perfectly average, no standout traits).

**Steps:**
1. Release film. Generate reviews.
2. Verify reviews are neutral/middling (e.g., "serviceable," "unremarkable," "fine").
3. No reviews should be extremely positive or negative (film is average).

**Expected Results:**
- Average films get average reviews.
- Review templates handle edge case gracefully.

**Severity if fails:** MEDIUM. Prevents review hyperbole for mediocre films.

---

## 4. INTEGRATION & EDGE CASE TESTING

These tests validate system interactions and hunt for exploits/failures.

### 4.1 Edge Case Battery

#### Test Case 4.1.1: Simultaneous 3-Film Production (Max Stress)
**Preconditions:**
- 3 active production slots unlocked.
- Greenlight 3 films simultaneously:
  - Film A: CG, $120M, 16-quarter pipeline.
  - Film B: 2D, $60M, 12-quarter pipeline.
  - Film C: Hybrid, $90M, 14-quarter pipeline.

**Steps:**
1. Advance full campaign. All 3 films overlap in Production phase.
2. Verify:
   - Resource allocation UI handles 3 films.
   - Render farm contention warnings appear.
   - Talent assignments don't double-book.
   - Quarterly tick performance acceptable (< 200ms on target hardware).
3. All 3 films release. Verify no data corruption in film records.

**Expected Results:**
- System handles max simultaneous productions.
- Performance remains acceptable.
- No crashes, no save corruption.

**Severity if fails:** CRITICAL. Max capacity must be stable.

#### Test Case 4.1.2: All-2D Studio Campaign
**Preconditions:**
- Never research CG tech. Only 2D branch.
- Greenlight only 2D films.

**Steps:**
1. Play through 1995-2010 with 2D-only strategy.
2. Verify:
   - 2D films become less profitable after 2003 (market shift).
   - ARTISTIC COURAGE reputation rises.
   - Prestige Directors seek player studio.
   - Late-game: 2D Master Suite tech allows competitive ANIMATION QUALITY.
   - Awards winnable (if STORY/HEART high).
3. Campaign completable without bankruptcy (hard but viable).

**Expected Results:**
- 2D-only strategy is mechanically viable (harder, not impossible).
- Player feels artistic conviction, not punished for bad choice.

**Severity if fails:** HIGH. 2D path must be real, not trap.

#### Test Case 4.1.3: Sequel-Only Strategy
**Preconditions:**
- First film succeeds ($200M+ gross, REWATCHABILITY 7+).

**Steps:**
1. Greenlight sequel. Verify:
   - Sequel costs 70% of original budget (reusable assets).
   - Opening weekend 120% of original.
   - ORIGINALITY capped at 5.
2. Greenlight 2nd sequel. Verify:
   - Franchise fatigue: gross -15% from first sequel.
   - ORIGINALITY capped at 3.
3. Greenlight 3rd sequel. Verify:
   - Fatigue: gross -15% from 2nd sequel.
   - ORIGINALITY capped at 2.
   - Projector Score suffers (low ORIGINALITY hurts critics).
4. Verify 3rd sequel is roughly break-even or loss. 4th sequel is unprofitable.

**Expected Results:**
- First sequels are profitable.
- Over-sequelizing has diminishing returns.
- Franchise fatigue is real mechanical brake.

**Severity if fails:** HIGH. Sequels must be tempting but self-limiting.

#### Test Case 4.1.4: Bankruptcy Recovery
**Preconditions:**
- Trigger CRISIS MODE (budget < -$30M).

**Steps:**
1. Accept emergency loan ($40M).
2. Lay off 30% staff (forced).
3. Cancel 1 active film (sunk costs lost).
4. Verify budget stabilizes (~$5M after loan).
5. Continue campaign. Release next film with -10% revenue penalty (loan terms).
6. Verify recovery is possible (not death spiral).

**Expected Results:**
- Crisis is painful but survivable.
- Player can recover with smart decisions.

**Severity if fails:** HIGH. Bankruptcy shouldn't be game over.

#### Test Case 4.1.5: Min-Spec Hardware Performance
**Preconditions:**
- Test machine: Intel UHD 620 (integrated GPU), i5-8250U, 8GB RAM.

**Steps:**
1. Load late-game save (Q50, 3 active films, 50+ staff).
2. Advance quarters. Measure frame rate and quarterly tick time.
3. Verify:
   - Maintain 60fps in UI (or 30fps if targeting lower).
   - Quarterly tick < 200ms.
   - No memory leaks (RAM usage stable over 30 minutes).

**Expected Results:**
- Game playable on min-spec hardware.
- Performance meets targets.

**Severity if fails:** HIGH. Excludes large player base if unplayable on min-spec.

#### Test Case 4.1.6: Save/Load Mid-Production
**Preconditions:**
- Film in Production, Quarter 3 of 5. Decision history includes 15 decisions.

**Steps:**
1. Save game.
2. Load save.
3. Verify:
   - Film phase, quarters remaining, DNA scores identical.
   - Decision history intact (all 15 decisions listed).
   - Assigned talent still assigned.
   - Budget matches.
4. Advance 1 quarter, save again. Compare two saves (should differ only by 1 quarter advance, deterministic).

**Expected Results:**
- Save/load preserves full simulation state.
- No data loss or corruption.

**Severity if fails:** CRITICAL. Save corruption is unacceptable.

### 4.2 Exploit Hunting

#### Test Case 4.2.1: Infinite Money Exploit Search
**Preconditions:**
- Look for any revenue source that can be abused.

**Steps:**
1. Test: Greenlight film, cancel during Development (before major costs). Do sunk costs return?
   - Expected: No refund. Costs are committed.
2. Test: Merchandise licensing. Can player trigger multiple times for same film?
   - Expected: Merchandise pays out once, then done.
3. Test: Home video revenue timing. Can player manipulate by save/load?
   - Expected: Revenue locked to release quarter + 2. No manipulation.

**Expected Results:**
- No infinite money exploits.
- All revenue sources have limits.

**Severity if fails:** HIGH. Economic exploits break game balance.

#### Test Case 4.2.2: DNA Score Manipulation
**Preconditions:**
- Look for ways to max all DNA scores (should be impossible).

**Steps:**
1. Test: Maximal investment in all phases. Can film have 10.0 in all 8 DNA scores?
   - Expected: No. Tradeoffs exist (e.g., tone calibration forces HUMOR vs. HEART choice).
2. Test: Retroactive tech application spam. Apply all tech to one film.
   - Expected: Costs and delays stack. Financially ruinous.

**Expected Results:**
- Perfect films are impossible (by design).
- Tradeoffs enforced.

**Severity if fails:** MEDIUM. Removes strategic tension if exploitable.

#### Test Case 4.2.3: Crunch Without Consequences
**Preconditions:**
- Attempt to crunch indefinitely without morale/culture penalties.

**Steps:**
1. Activate crunch for 5 consecutive quarters.
2. Verify:
   - Morale plummets.
   - Studio culture crisis triggers.
   - Animators quit.
   - Future hiring costs increase.

**Expected Results:**
- Crunch has escalating, unavoidable costs.

**Severity if fails:** HIGH. Crunch must be balanced risk, not free boost.

---

## 5. RISK ASSESSMENT & CRITICAL FAILURE MODES

### 5.1 High-Risk Systems

| System | Risk | Consequence if Broken | Mitigation Priority |
|--------|------|----------------------|-------------------|
| **Film DNA Scoring** | Non-deterministic results, opaque attribution | Players can't learn, optimization impossible | HIGHEST |
| **Box Office Formulas** | Imbalanced (all strategies converge to same result) | Strategic depth collapses | HIGHEST |
| **Save/Load** | Corruption, desync | Lost progress, 1-star reviews | HIGHEST |
| **Economy** | Exploits or death spirals | Game too easy or too hard | HIGH |
| **Procedural Content** | Feels algorithmic, repetitive | Core fantasy (greenlight) loses magic | HIGH |
| **UI Performance** | Late-game slowdown on min-spec | Game unplayable for segment of audience | HIGH |

### 5.2 Medium-Risk Systems

| System | Risk | Consequence if Broken | Mitigation Priority |
|--------|------|----------------------|-------------------|
| **Rival AI** | Too weak/strong, not credible | Competition layer feels fake | MEDIUM |
| **Talent Poaching** | Doesn't happen or happens too often | Talent wars irrelevant or frustrating | MEDIUM |
| **Tech Tree Balance** | Dominant path (e.g., CG always best) | Strategic choice illusion | MEDIUM |
| **Crunch Mechanics** | Free speed or useless penalty | System ignored or abused | MEDIUM |

### 5.3 Low-Risk Systems

| System | Risk | Consequence if Broken | Mitigation Priority |
|--------|------|----------------------|-------------------|
| **Voice Actor Scheduling** | Conflicts annoying, not strategic | Minor friction | LOW |
| **Marketing Phase** | Too simple or too complex | One phase of six; fixable | LOW |
| **Diegetic UI Aesthetics** | Looks worse than mockups | Polish issue, not mechanical | LOW |

### 5.4 Critical Failure Modes (Showstoppers)

These bugs block release:

1. **Save corruption after 20+ hours.** Player loses campaign. Unforgivable.
2. **Non-deterministic simulation.** Same inputs, different outputs. Breaks trust.
3. **Soft-lock in production.** Film never completes, player can't advance. Dead save.
4. **Crash on release sequence.** Game crashes during box office gauntlet. Blocks progression.
5. **UI completely breaks on min-spec.** Game unplayable for target audience.
6. **Film DNA scoring is random.** Player has no idea why films succeed/fail. Core loop broken.

All other bugs are severity-tiered and can be patched post-launch if necessary.

---

## 6. QUALITY GATES (MUST PASS BEFORE ADVANCING)

### Gate 1: Prototype (Month 3)
**Criteria:**
- [ ] Film pipeline completes 1 full cycle (greenlight → release) without crashes.
- [ ] Film DNA scores are deterministic (same inputs = same outputs).
- [ ] Box office calculation matches formula (±1%).
- [ ] Decision attribution is legible (player can see why film scored X).
- [ ] Save/load preserves simulation state (no desync).
- [ ] 3 playtesters complete prototype loop, report feeling "creative stewardship."

**If fails:** Do not proceed to vertical slice. Fix core loop first.

### Gate 2: Vertical Slice (Month 6)
**Criteria:**
- [ ] 3-film campaign (1995-2003) playable start-to-finish.
- [ ] Diegetic studio UI functional (navigate rooms, interact with boards).
- [ ] Procedural film concepts feel authored (10+ playtesters review 50 concepts, 80%+ approval).
- [ ] Economy balanced (player can survive 3 films without exploits or guaranteed bankruptcy).
- [ ] UI performance: 60fps on target hardware during normal play.
- [ ] Zero critical bugs (crashes, soft-locks, save corruption).

**If fails:** Iterate on vertical slice. Do not expand to full campaign.

### Gate 3: Alpha (Month 10)
**Criteria:**
- [ ] Full 60-quarter campaign playable (2 complete playthroughs, varied strategies).
- [ ] All 8 DNA scores validated (interaction effects work as designed).
- [ ] Rival AI creates credible competition (2+ playtesters report rivals "feel real").
- [ ] Edge cases tested: all-2D studio, sequel-only studio, bankruptcy recovery (all completable).
- [ ] Performance at late-game acceptable (Q50+, 3 films, 60fps or 30fps on Switch).
- [ ] Procedural content quality: 100 film concepts + 25 review templates, no nonsensical output.
- [ ] Zero showstopper bugs.

**If fails:** Delay beta. Fix critical issues before QA certification prep.

### Gate 4: Beta (Month 12)
**Criteria:**
- [ ] Full regression suite passes (500+ test cases, 95%+ pass rate).
- [ ] Platform-specific testing complete (PC flawless, Switch/iPad at target perf).
- [ ] Save/load stress test: 100 save/load cycles across 60-quarter campaign, zero corruption.
- [ ] Contract QA team clears game for submission (no P1/P2 bugs remaining).
- [ ] Steam integration tested (achievements unlock, cloud save works).
- [ ] Localization hooks validated (all text externalized, ready for translation).
- [ ] Zero P1/P2 bugs. P3 bugs triaged for patch.

**If fails:** Delay launch. Ship when stable.

### Gate 5: Release Readiness (Month 13)
**Criteria:**
- [ ] Day-one patch tested and ready (if needed).
- [ ] Steam page live, trailer approved.
- [ ] Press keys distributed, embargo coordinated.
- [ ] Community management plan active (Discord, subreddit moderated).
- [ ] Rollback plan documented (if launch goes wrong, can we revert?).

**If fails:** Delay launch window.

---

## 7. REGRESSION TESTING FRAMEWORK

### 7.1 Automated Unit Tests (Programmer Responsibility)

These run nightly on CI/CD:

- **Film DNA Scoring:** 50 test cases with fixed inputs, assert exact outputs.
- **Box Office Formulas:** 30 test cases covering edge cases (competition, season modifiers, variance).
- **Economy Calculations:** 40 test cases (quarterly expenses, revenue flow, bankruptcy threshold).
- **Tech Tree Prerequisites:** 20 test cases (validate dependency chains).
- **Talent Poaching Probability:** 15 test cases (morale/salary thresholds).
- **Save/Load Determinism:** 10 test cases (save, load, advance 1 quarter, compare).

**Target:** 95%+ pass rate on nightly runs. Failures block morning standup until resolved.

### 7.2 Manual Regression Suite (QA Responsibility)

Run weekly during alpha/beta:

- **Core Loop Validation:** Greenlight 1 film, complete production, release. 20 minutes.
- **Multi-Film Stress Test:** 3 simultaneous films, advance 20 quarters. 30 minutes.
- **Edge Case Sampling:** Test 3 edge cases from Section 4.1 (rotate weekly). 60 minutes.
- **Procedural Content Spot Check:** Generate 20 concepts, 10 reviews. Verify quality. 15 minutes.
- **UI Smoke Test:** Navigate all studio rooms, trigger all major screens. 10 minutes.
- **Save/Load Cycle:** Save, load, verify state. 5 minutes.

**Total weekly regression time:** ~2.5 hours. Run every Friday before weekend build.

### 7.3 Platform-Specific Testing (Contract QA, Month 11-12)

**PC (Steam):**
- Resolution scaling (1280×720 to 4K).
- Controller support (Xbox, PlayStation, generic).
- Alt-tab, minimize, windowed mode stability.
- Multi-monitor setups.
- Steam overlay compatibility.

**Nintendo Switch:**
- Handheld vs. docked performance.
- Sleep/wake stability (suspend during quarterly tick, resume, verify no crash).
- Joy-Con drift tolerance.
- Memory leak testing (3-hour session, check RAM usage).
- Lotcheck compliance (button prompts, terminology, crashes).

**iPad (if applicable):**
- Touch target size (44pt minimum per Apple HIG).
- Pinch-to-zoom (if implemented).
- App lifecycle (background, foreground, termination, resume).
- iOS versions (test on iOS 16, 17).

---

## 8. PERFORMANCE BENCHMARKS

### 8.1 Target Metrics

| Metric | PC (Target) | Switch (Target) | iPad (Target) |
|--------|-------------|-----------------|---------------|
| Frame Rate | 60fps | 30fps | 60fps |
| Quarterly Tick Time | < 100ms | < 200ms | < 150ms |
| Save Time (Q60) | < 200ms | < 500ms | < 300ms |
| Load Time (Q60) | < 100ms | < 300ms | < 150ms |
| Memory Usage | < 2GB | < 2GB | < 1.5GB |
| Draw Calls (Studio View) | < 50 | < 30 | < 40 |

### 8.2 Performance Profiling Plan

**Phase 1 (Month 3):** Prototype performance baseline.
- Profile quarterly tick (10 films processed).
- Profile save/load (small state, Q10).
- Identify hottest code paths.

**Phase 2 (Month 6):** Vertical slice optimization.
- Profile UI rendering (production board with 3 films).
- Measure draw calls, SetPass calls, canvas rebuilds.
- Optimize if exceeding targets.

**Phase 3 (Month 10):** Late-game stress test.
- Profile at Q50 (3 active films, 50+ staff, full tech tree).
- Measure memory usage over 1-hour session (check for leaks).
- Amortize quarterly tick if exceeds 100ms.

**Phase 4 (Month 12):** Platform-specific tuning.
- Switch: profile on devkit, reduce particle complexity if needed.
- iPad: offload more work to background threads.

### 8.3 Optimization Fallbacks

If performance targets are missed:

1. **Quarterly tick too slow:**
   - Amortize across 3-5 frames (show "Processing Quarter..." spinner).
   - Cache frequently-accessed calculations (Film DNA composites).

2. **UI frame rate drops:**
   - Reduce canvas complexity (fewer nested layout groups).
   - Disable particle effects on lower-end hardware.
   - Reduce animation frame rate (30fps UI on Switch).

3. **Save/load too slow:**
   - Compress JSON with GZip (70% size reduction).
   - Async save on background thread.

4. **Memory leaks:**
   - Profile with Unity Profiler (Memory module).
   - Check for untracked MonoBehaviour references, event listener leaks.

---

## 9. BUG TRIAGE & SEVERITY DEFINITIONS

### 9.1 Severity Levels

**P0 - SHOWSTOPPER (Ship-blocking):**
- Crash on launch.
- Save file corruption (progress loss).
- Soft-lock (player cannot advance, save is dead).
- Critical system completely broken (e.g., films never release).

**Response:** Drop everything. Fix immediately. All hands.

**P1 - CRITICAL (Blocks major functionality):**
- Feature doesn't work (e.g., tech tree research doesn't unlock nodes).
- Frequent crashes (repro rate > 50%).
- Major UI bug (screen unreadable, buttons don't respond).
- Exploit that breaks game balance (infinite money).

**Response:** Fix before next milestone gate. Daily standup priority.

**P2 - HIGH (Impacts experience significantly):**
- Intermittent crashes (repro rate 10-50%).
- DNA scoring feels random (attribution unclear).
- Rival AI doesn't compete.
- Performance below target on primary platform.

**Response:** Fix during current phase. Address in weekly sprint.

**P3 - MEDIUM (Noticeable but not blocking):**
- UI polish issues (text overflow, alignment).
- Minor calculation errors (off by 1-2%).
- Content quality issues (1-2 bad film concepts out of 100).
- Controller navigation awkward.

**Response:** Fix if time permits. Triage for post-launch patch.

**P4 - LOW (Cosmetic or rare):**
- Typos in flavor text.
- Animation glitches (visual only, no gameplay impact).
- Rare edge case (repro rate < 1%).

**Response:** Log, triage post-launch or ignore.

### 9.2 Bug Reporting Template

```
**Title:** [Brief description]

**Severity:** [P0/P1/P2/P3/P4]

**Repro Rate:** [100% / 50% / 10% / Rare]

**Platform:** [PC / Switch / iPad]

**Build:** [Version number, commit hash]

**Preconditions:**
- [What state the game must be in]

**Steps to Reproduce:**
1. [Step 1]
2. [Step 2]
3. [Step 3]

**Expected Result:**
- [What should happen]

**Actual Result:**
- [What actually happens]

**Screenshots/Video:**
- [Attach if applicable]

**Save File:**
- [Attach if crash/corruption]

**Logs:**
- [Unity Player.log or device logs]
```

### 9.3 Triage Meeting Cadence

**Daily (during Beta):** Review all new P0/P1 bugs. Assign immediately.

**Weekly (during Alpha):** Review all P2 bugs. Prioritize for sprint.

**Bi-weekly (during Alpha):** Review P3/P4 backlog. Close duplicates, defer low-priority.

---

## 10. PLAYTESTING PLAN

### 10.1 Internal Playtests (Team)

**Frequency:** Weekly, starting Month 4 (vertical slice).

**Duration:** 60-90 minutes per session.

**Focus Areas:**
- Is the core loop fun?
- Are decisions meaningful?
- Can players explain why their films succeeded/failed?
- Are there soft-locks or exploits?

**Deliverable:** Written feedback + bug reports (use template from Section 9.2).

### 10.2 External Playtests (Recruited Testers)

**Frequency:** Monthly, starting Month 6.

**Recruits:**
- 10-15 players from target audience (management sim fans, game dev/film enthusiasts).
- Mix of skill levels (novice sim players, expert min-maxers).

**Format:**
- Send build + questionnaire.
- 2-hour session (recorded if possible).
- Post-session survey + interview (30 min).

**Survey Questions:**
1. Did you understand why your films succeeded or failed? (Yes/No + explain)
2. Rate decision meaningfulness (1-5 scale).
3. What was the most frustrating moment?
4. What was the most satisfying moment?
5. Would you recommend this to a friend? (Yes/No + why)

**Success Criteria:**
- 80%+ answer "Yes" to question 1 (decision legibility).
- Average 4+ on question 2 (meaningful decisions).
- Zero reports of soft-locks or game-breaking bugs.

### 10.3 Closed Beta (Month 12)

**Recruits:** 100-200 players via email list, Discord, subreddit.

**Format:**
- Steam beta branch (or TestFlight for iPad).
- Open-ended play (no time limit).
- Bug reporting via Google Form.
- Community Discord for real-time feedback.

**Goals:**
- Stress test save/load across diverse hardware.
- Hunt for edge cases and exploits.
- Validate late-game balance (most testers won't finish, but some will).

**Success Criteria:**
- Zero P0/P1 bugs reported.
- < 5 P2 bugs reported.
- Community sentiment positive (Discord vibes, bug report tone).

---

## 11. CERTIFICATION READINESS (PLATFORM-SPECIFIC)

### 11.1 Steam (PC)

**Requirements:**
- No DRM beyond Steam (optional: Steamworks API for achievements).
- Stable on Windows 10/11 (primary), macOS (secondary).
- Controller support (Steam Input API).
- Cloud save integration (Steamworks).
- Trading cards, achievements (optional but recommended).

**Pre-Launch Checklist:**
- [ ] Steam page live (capsule art, trailer, description).
- [ ] Build uploaded to Steamworks (depot configured).
- [ ] Achievements tested (unlock correctly, sync to Steam).
- [ ] Cloud save tested (sync across machines).
- [ ] Press build tested (no debug UI, no test accounts).

**Common Issues:**
- Achievements not unlocking → verify Steam API initialized before calls.
- Cloud save conflicts → test save/load on two machines, verify sync.

### 11.2 Nintendo Switch

**Requirements:**
- Nintendo Developer license (approved by Nintendo).
- Lotcheck submission (Nintendo's QA certification).
- ESRB rating (required for US release).
- Compliance with Nintendo guidelines (button prompts, terminology, stability).

**Lotcheck Focus Areas:**
- **Suspend/Resume:** Game must handle sleep mode gracefully (no crashes, no data loss).
- **Button Prompts:** Must use Nintendo-approved button icons and terminology ("Press A" not "Press X").
- **Crashes:** Zero tolerance. Any crash during lotcheck = fail.
- **Memory:** Game must not exceed RAM limits. Test for leaks.
- **Save Data:** Must use Nintendo's save API. Corruption = fail.

**Pre-Submission Checklist:**
- [ ] Test suspend/resume during quarterly tick, production phase, box office sequence.
- [ ] Verify all button prompts match Nintendo style guide.
- [ ] Run 3-hour stress test (check for memory leaks, crashes).
- [ ] Submit ROM to Nintendo partner portal.

**Lotcheck Timeline:** 4-6 weeks. Plan accordingly.

### 11.3 iPad (iOS)

**Requirements:**
- Apple Developer account ($99/year).
- App Review (Apple's approval process).
- Privacy manifest (iOS 17+ requirement).
- Universal build (iPhone + iPad support, or iPad-only).

**App Review Focus Areas:**
- **Crashes:** Zero tolerance.
- **Privacy:** If collecting data, must declare. FRAMEWAR collects none → minimal compliance.
- **Metadata Accuracy:** Screenshots, description must match gameplay.
- **In-App Purchases:** Not applicable (premium pricing, no IAP).

**Pre-Submission Checklist:**
- [ ] Build uploaded to App Store Connect.
- [ ] TestFlight beta tested (10+ testers, 1 week minimum).
- [ ] Privacy manifest included (declares no data collection).
- [ ] Screenshots + App Preview video prepared (6.5" and 12.9" sizes).
- [ ] Submit for review.

**App Review Timeline:** 1-3 days (usually fast for premium games).

---

## 12. POST-LAUNCH SUPPORT PLAN

### 12.1 Day-One Patch Readiness

**If critical bug discovered post-launch:**
- Hotfix build prepared within 24 hours.
- Steam: push to default branch immediately.
- Switch: submit emergency patch (Nintendo fast-track: 1-2 weeks).
- iPad: submit urgent patch (Apple can expedite: 1-3 days).

**Pre-Launch Preparation:**
- [ ] Rollback build archived (last known stable).
- [ ] Patch deployment process documented.
- [ ] Community communication plan (Discord announcement, Steam post).

### 12.2 Balance Patches (Post-Launch Months 1-3)

**Data Collection:**
- Track player film releases: DNA scores, box office results, strategies.
- Identify dominant strategies (e.g., "everyone goes CG, nobody touches 2D").
- Survey community: what feels unfair, too easy, too hard?

**Patch 1.1 (Month 1):**
- Formula tweaks (e.g., if SPECTACLE dominates, reduce its box office weight).
- Tech tree cost adjustments (e.g., if 2D is never researched, make it cheaper).
- UI polish (text overflow fixes, button hitboxes).

**Patch 1.2 (Month 2):**
- Additional content (20 new film concepts, 5 new tech nodes).
- Rival AI tuning (if too weak/strong based on feedback).

**Patch 1.3 (Month 3):**
- Quality-of-life improvements (e.g., "speed up" button for veteran players, tooltips for complex systems).

### 12.3 Community Management

**Platforms:**
- Discord server (moderated daily).
- Subreddit (check twice daily).
- Steam forums (respond to bug reports within 24 hours).

**Response Protocols:**
- **Bug reports:** Acknowledge within 24h, provide ETA for fix.
- **Balance complaints:** Gather data, respond with analysis (not defensive).
- **Feature requests:** Log in backlog, no promises unless feasible.

### 12.4 DLC/Expansion (Optional, Month 6+)

**"Streaming Wars" Expansion:**
- Extends timeline to 2020.
- Adds streaming platform competition (Netflix, Disney+, etc.).
- New tech tree branch (real-time rendering, episodic content).
- New rival studios (streaming-first competitors).

**Scope:** 3-4 months development, $5-10 price point.

**Viability depends on:** Base game sales (10k+ units = greenlight expansion).

---

## 13. OPEN QUESTIONS & RISKS

### 13.1 Unresolved Design Questions That Affect QA

**Q1: How granular should the Production Pipeline phase gates be?**
- Current design: 3-5 decisions per phase.
- Risk: Too many decisions = tedium. Too few = shallow.
- **QA Impact:** If gates feel tedious, playtesters will report. Need 10+ playthroughs to calibrate.

**Q2: Should Studio Soul be visible or hidden?**
- Current design: Hidden. Player infers from effects.
- Risk: If too hidden, feels arbitrary. If visible, invites min-maxing.
- **QA Impact:** Test both in A/B playtest. Measure player comprehension of studio identity.

**Q3: What's the right campaign length?**
- Current target: 8-12 hours (60 quarters).
- Risk: Too short = identity arc doesn't develop. Too long = mid-campaign sag.
- **QA Impact:** Instrument playtests. Log when players pause, speed up, or alt-tab. Identify boring stretches.

**Q4: How aggressive should Rival AI be?**
- Current design: Moderate. Rivals compete but don't dominate.
- Risk: Too weak = boring. Too strong = frustrating.
- **QA Impact:** Need difficulty tuning based on win/loss rates across 20+ full campaigns.

### 13.2 Technical Risks That Need Validation

**R1: Simulation Determinism**
- **Risk:** Hidden non-determinism (time-based RNG, floating-point drift).
- **Validation:** Automated test: save, load, advance 10 quarters, save again. Diff the two saves. Must be identical.
- **Mitigation:** Enforce seeded RNG, no UnityEngine.Random, no System.DateTime in sim logic.

**R2: UI Performance on Switch**
- **Risk:** Canvas rebuilds tank frame rate.
- **Validation:** Profile on Switch devkit by Month 8. Measure draw calls, frame times.
- **Mitigation:** Aggressive canvas batching, static separation, reduce particles.

**R3: Procedural Content Quality**
- **Risk:** Film concepts feel algorithmic.
- **Validation:** 30-hour playtest with film-literate players. Survey: "Do concepts feel hand-written?" (target 80%+ yes).
- **Mitigation:** Hire writer to author 100+ templates with strong authorial voice.

**R4: Late-Game Economy Balance**
- **Risk:** Player too rich (trivial) or too poor (impossible) by Year 10.
- **Validation:** 10 full-campaign playthroughs with varied strategies. Track budget trajectories.
- **Mitigation:** Tune revenue/expense formulas based on data.

---

## 14. FINAL NOTES

This is a data-heavy simulation. Every bug is a systems bug. The QA strategy is:

1. **Validate math first.** Unit test all formulas. If the math is wrong, everything downstream is wrong.
2. **Test determinism obsessively.** Non-deterministic sims are untestable. Save/load must be byte-perfect.
3. **Playtest for legibility, not just functionality.** The game can "work" and still fail if players can't understand why. Test comprehension, not just mechanics.
4. **Hunt exploits like your job depends on it.** Because it does. Players will find the optimal strategy in Week 1. If it's degenerate, the game is boring.
5. **Performance at scale is non-negotiable.** Late-game (Q50+, 3 films) must be as smooth as early-game. Profile early, optimize often.

The game lives or dies on one question: **Can the player look at a film's DNA scores and understand the story of how it was made?** If yes, the simulation has authorial weight. If no, it's a spreadsheet with a skin.

Test for that. Everything else is downstream.

---

**End of QA Plan**

---

**Test Coverage Summary:**
- **Core Systems:** 40 test cases (Film Pipeline, DNA, Box Office, Talent, Tech Tree, Economy, AI, Procedural)
- **Edge Cases:** 6 major scenarios (3-film stress, all-2D, sequel-only, bankruptcy recovery, min-spec, save/load)
- **Exploit Hunting:** 3 vectors (money, DNA, crunch)
- **Performance:** 6 benchmarks across 3 platforms
- **Regression:** 200+ automated unit tests, 15-hour weekly manual suite

**Estimated QA Hours (Full Campaign):**
- Prototype (Months 1-3): 40 hours
- Vertical Slice (Months 4-6): 80 hours
- Alpha (Months 7-10): 200 hours
- Beta (Months 11-12): 150 hours
- Certification (Month 13): 60 hours
- **Total:** ~530 hours QA (roughly 3 months full-time QA lead + 2 months contract QA)

**Absolute file paths referenced:**
- /Users/burcukose/git/project-draft/games/12-framewar/pitch.md
- /Users/burcukose/git/project-draft/games/12-framewar/game-design.md
- /Users/burcukose/git/project-draft/games/12-framewar/narrative-bible.md
- /Users/burcukose/git/project-draft/games/12-framewar/technical-architecture.md
- /Users/burcukose/git/project-draft/games/12-framewar/qa-plan.md (this document)
