# FRAMEWAR — Production Plan

**Producer**: CLOCK
**Version**: 1.0
**Date**: 2026-02-07
**Project Status**: Pre-Production Complete, Production Planning Active

---

## 1. PROJECT OVERVIEW

### 1.1 What We're Shipping

**Title**: FRAMEWAR
**Genre**: Animation Studio Management Simulation
**Platform(s)**: PC (Steam) primary, Nintendo Switch secondary, iPad tertiary
**Engine**: Unity 2022.3 LTS
**Target Audience**: Management sim players (Game Dev Tycoon, Two Point Hospital), film/animation enthusiasts, creative professionals
**Campaign Length**: 8-12 hours (1995-2010 timeline, 60 in-game quarters)
**Team Size**: 4 core + contractors
**Timeline**: 15 months (63 weeks)
**Budget**: $180k-$240k

### 1.2 The Scope Lock

This is not pitch-phase dreaming. This is what we're building.

**Core Features (Non-Negotiable):**
1. Film Production Pipeline (6 phases: DEV, PRE, PROD, POST, MKT, REL)
2. Diegetic Studio Interface (corkboard greenlight table, physical production board, screening room)
3. Film DNA System (8 attributes, procedural scoring with decision attribution)
4. Talent Engine (Directors, Animators, Story Artists, Voice Actors with morale/loyalty)
5. Technology Tree (CG branch, 2D branch, Hybrid branch — 40 nodes total)
6. Box Office Gauntlet (4-week release simulation, critic/audience scores, awards)
7. Rival Studio AI (3 rival studios with distinct strategies)
8. Era Simulation (1995-2010 with historical events, tech evolution, market shifts)

**Cut Features (Not In v1.0):**
- Actually watching the films (abstraction only)
- Live-action productions (animation only)
- Online multiplayer
- Voice acting mini-games
- Real celebrity/studio names (all fictional)
- Studio architecture design (pre-designed spaces)

**Stretch Goals (Post-Launch or DLC):**
1. Studio Culture System (crunch mechanics, workplace health)
2. Sequel Machine (franchise management)
3. Press Tour mini-game
4. Director's Cut mode
5. Industry Events (procedural disruptions)
6. Modding support

### 1.3 The Reality Check

**What Could Kill This Project:**
1. Scope creep (adding "just one more feature" in Month 8)
2. Procedural content that feels algorithmic (kills emotional investment)
3. UI performance issues on Switch (forces platform cut)
4. Mid-campaign sag (Hours 4-7 feel repetitive)
5. Box office formula balance (all films succeed or all fail predictably)

**What We're Doing About It:**
1. Feature freeze at end of Alpha (Month 10). No exceptions.
2. Writer-authored content templates + extensive playtesting (3 full campaign runs minimum)
3. Profile on Switch devkit by Month 3. Cut platform if perf doesn't hit 30fps by Month 6.
4. Era 3 crisis events designed explicitly to break routine (2D collapse, rival mega-hit, studio crisis)
5. Spreadsheet modeling + player data collection during Beta

### 1.4 Team Structure

**Core Team:**
- **BYTE** (Lead Programmer) — 1.0 FTE, 15 months
  - All simulation systems, Unity integration, save/load, tools
- **PIXEL** (Art Director) — 1.0 FTE, 12 months (Months 1-12)
  - Diegetic UI, studio environments, character portraits, iconography
- **ECHO** (Sound Designer) — 0.5 FTE, 9 months (Months 4-12)
  - SFX library, ambience, FMOD integration, music direction
- **REED** (Lead Designer) — 0.5 FTE, 15 months
  - Systems design, balance tuning, content authoring (film concepts, tech tree)

**Contractors:**
- Composer (Months 8-12, 200 hours, $12k)
- Writer (Months 4-8, 150 hours, $9k for review templates and concept polish)
- QA Lead (Months 11-12, 320 hours, $16k)
- Playtester Pool (Months 6-12, 10 testers, $50/session, ~$8k)

**Total Headcount:** 4 core + 4 contractors

---

## 2. MILESTONE DEFINITIONS

### MILESTONE 1: PROTOTYPE (Months 1-3, Weeks 1-12)

**Entry Criteria:**
- Team assembled
- Unity project initialized
- Git repo configured with LFS
- Design docs complete (pitch, GDD, narrative bible)

**Exit Criteria (All Must Pass):**
- ✓ Player can greenlight a film, make production decisions, see box office results
- ✓ Film DNA scores are deterministic and legible (post-mortem explains outcomes)
- ✓ One complete film cycle playable in 15-20 minutes
- ✓ Save/load functional (JSON serialization working)
- ✓ Core loop validation: 5 playtesters report "creative stewardship" feeling
- ✓ Unit tests pass for Film DNA calculation (fixed inputs = fixed outputs)
- ✓ Zero critical bugs (no crashes, no save corruption)

**Deliverables:**
1. FilmSimulator service (all 6 phases, simplified decisions)
2. BoxOfficeSimulator service (revenue calculation, Projector Score, reviews)
3. Text-based prototype UI (no diegetic studio yet — menus and tables)
4. Greenlight decision flow (concept cards -> greenlight -> production starts)
5. Production Pipeline Board (basic phase progression visualization)
6. Box Office Results screen (numbers + procedural reviews)
7. Save/load system (manual save/load buttons)
8. 10 film concept templates (tested for quality)
9. 5 review templates (tested for variety)

**Key Decisions Required:**
- Decision density per phase: Is 3-5 decisions correct, or should we go to 2-3? (Decision by Week 8 playtest)
- Determinism validation: Are all systems using seeded RNG correctly? (Code review Week 10)

**Risk Mitigation:**
- **Risk**: Simulation feels random, not responsive to player decisions
  - **Mitigation**: Decision attribution tracking from Day 1. Every DNA score change logged with source decision.
- **Risk**: Core loop takes too long (>30 minutes per film)
  - **Mitigation**: Timebox production decisions. If one phase exceeds 5 minutes, simplify.

### MILESTONE 2: VERTICAL SLICE (Months 4-6, Weeks 13-26)

**Entry Criteria:**
- Prototype exit criteria met
- Diegetic UI art style locked (corkboard aesthetic, studio room concepts approved)
- Audio direction doc complete

**Exit Criteria:**
- ✓ 3-film campaign arc playable in 90 minutes (1995-2003)
- ✓ Diegetic studio UI implemented (Greenlight Office, Production Board Room, Screening Room, Render Farm visible)
- ✓ Talent hiring/management functional (hire Director, assign Animators, morale tracking)
- ✓ Tech Tree functional (20 nodes, research mechanics, tech effects apply to films)
- ✓ Budget simulation creates tension (10 playtesters report "meaningful resource management")
- ✓ 2 rival studios release films that compete with player
- ✓ 30 film concept templates + 10 review templates feel "authored, not algorithmic" (qualitative playtest validation)
- ✓ UI performance: 60fps on PC (GTX 1060 equivalent) during normal play
- ✓ Save/load tested for 3-film campaign (no corruption)

**Deliverables:**
1. Diegetic Studio View (isometric camera, room navigation)
2. Corkboard Greenlight Table (physical pin/paper aesthetic)
3. Production Pipeline Board (film cards move through phases)
4. Screening Room (Box Office Gauntlet presentation)
5. Render Farm visualization (monitors, progress bars)
6. Talent Hiring UI (Talent Agency Board with portrait cards)
7. TalentManager service (morale, poaching, assignment)
8. TechTree service + UI (node graph, research queue)
9. EconomyCalc service (budget tracking, quarterly burn)
10. RivalAI basic behavior (2 rivals with simplified strategies)
11. 30 film concept templates (covering major genres/tones)
12. 10 review templates (covering score ranges and DNA profiles)
13. Audio implementation begins (FMOD setup, basic SFX)
14. Character portrait library (20 Directors, 30 Animators as test set)

**Key Decisions Required:**
- Studio navigation: Click-to-enter rooms or free camera pan? (Decision by Week 16)
- Tech Tree layout: Grid or organic node graph? (Decision by Week 18, based on readability test)
- Rival release timing: How aggressive should competition be? (Tuning by Week 24 playtest)

**Risk Mitigation:**
- **Risk**: Diegetic UI looks good but is hard to navigate
  - **Mitigation**: Usability testing Week 20. 5 new players (no prior exposure) must complete greenlight->release flow without help.
- **Risk**: Procedural content still feels generic
  - **Mitigation**: Bring in contract writer Week 16. Review all 30 templates for narrative voice. Iterate until "sounds like a passionate pitch."
- **Risk**: UI performance misses 60fps target
  - **Mitigation**: Profiling sprint Week 22. Canvas batching, draw call audit, particle reduction. If still under target, cut particle effects.

### MILESTONE 3: ALPHA (Months 7-10, Weeks 27-43)

**Entry Criteria:**
- Vertical Slice exit criteria met
- All core systems prototyped and validated
- Full content scope locked (100 concepts, 25 reviews, 40 tech nodes, 50 Directors, 100 Animators)

**Exit Criteria:**
- ✓ Full 60-quarter campaign playable (1995-2010, 6-10 films)
- ✓ All 8 core features complete and integrated
- ✓ Content complete: 100 film concepts, 25 review templates, 40 tech nodes, full talent database
- ✓ 3 rival studios with distinct strategies (Prestige, Commercial, Franchise)
- ✓ Era events trigger correctly (2D collapse 2003, Oscar creation 2001, etc.)
- ✓ Studio Soul system functional (hidden axis affects talent/pitches/reviews)
- ✓ Awards season simulation (Best Animated Feature from 2001 onward)
- ✓ End-game retrospective screen (legacy summary)
- ✓ 3 full campaign playtests complete without blocking bugs
- ✓ Mid-campaign sag addressed (Era 3 creates tension, not tedium)
- ✓ UI polish pass 1: animations, transitions, particle effects
- ✓ Audio: 300+ SFX assets, ambience layers per room, adaptive music stems (5 themes)
- ✓ Performance: 60fps on PC with 3 simultaneous films, 50+ staff, full tech tree

**Deliverables:**
1. Studio Soul system (decision tracking, reputation effects)
2. Sequel/franchise mechanics
3. Awards season (nomination/winner simulation, Oscar ceremony presentation)
4. Director morale showdowns (override consequences)
5. Test screening system (focus group results, re-cut decisions)
6. Era event system (triggered events per timeline)
7. End-game retrospective (procedural legacy summary)
8. 100 film concept templates (full coverage of genre/tone/risk matrix)
9. 25 review templates (all DNA profile archetypes covered)
10. 40 tech tree nodes (complete CG, 2D, Hybrid branches)
11. 50 Director profiles (full trait variation)
12. 100 Animator profiles
13. 80 Voice Actor profiles
14. UI animation pass (card transitions, number count-ups, phase completion effects)
15. SFX library (300+ assets: UI, ambience, events, production)
16. Adaptive music system (5 themes with 4-6 layers each, FMOD implementation)
17. 6 scripted music cues (First Greenlight, Oscar Win, 2D Division Closes, etc.)

**Key Decisions Required:**
- Sequel fatigue curve: What's the gross reduction per sequel? (Spreadsheet modeling + playtest data by Week 35)
- Studio Soul threshold effects: At what SOUL values do consequences trigger? (Playtest tuning by Week 38)
- Awards algorithm: Is the weighted formula producing believable winners? (10 simulated awards seasons by Week 40)

**Risk Mitigation:**
- **Risk**: Mid-campaign sag (Hours 4-7 feel repetitive)
  - **Mitigation**: Era 3 event density increased. 2D collapse is mandatory crisis. Rival mega-hit shakes up market. Player must adapt or die.
- **Risk**: Late-game performance degrades (3 films + 50 staff = frame drops)
  - **Mitigation**: Profiling Week 38. Amortize quarterly tick across 3-5 frames if needed. Show "Processing..." spinner.
- **Risk**: Content authoring falls behind schedule
  - **Mitigation**: Content creation starts Week 27 (early in Alpha). Writer contract extended if needed. Fallback: ship with 80 concepts instead of 100 (still viable).

### MILESTONE 4: BETA (Months 11-12, Weeks 44-52)

**Entry Criteria:**
- Alpha exit criteria met
- All features complete (feature freeze enforced)
- Steam page live (capsule art, trailer, description)

**Exit Criteria:**
- ✓ Zero critical bugs (crashes, save corruption, progression blockers)
- ✓ All playtest feedback addressed or logged as post-launch
- ✓ Performance meets targets: 60fps PC, 30fps Switch (if platform viable)
- ✓ Full QA pass complete (regression suite, edge cases, 10+ full campaigns)
- ✓ Save/load stress-tested (Q60 saves, load at every quarter, no corruption)
- ✓ Steam integration complete (achievements, cloud save, rich presence)
- ✓ Trailer and key art finalized
- ✓ Localization-ready (string tables externalized, even if not translated yet)
- ✓ Balance validated (spreadsheet models match player behavior data)
- ✓ 5 "blind" playtesters (no dev contact) complete campaign and provide feedback

**Deliverables:**
1. Full QA regression suite (automated where possible)
2. Edge case testing (bankrupt recovery, all-2D campaign, sequel-only strategy, max crunch)
3. Save/load stress testing (save/load at every quarter of 60-quarter campaign)
4. Performance optimization pass (profiler-guided)
5. Canvas batching optimization (draw calls <50, SetPass calls <10)
6. Quarterly tick amortization (spread across 3-5 frames if needed)
7. Platform builds (Windows x64, macOS if time permits, Switch if perf acceptable)
8. Steam integration (achievements 30-40, cloud save, rich presence, trading cards optional)
9. Trailer (2 minutes, focus on diegetic UI and decision moments)
10. Steam capsule art (studio at night, production board, warm lighting)
11. Press kit (fact sheet, screenshots, GIFs, press release)
12. Influencer key distribution (50 keys to YouTube/Twitch management sim streamers)
13. Balance patch prep (data-driven formula adjustments based on playtest data)

**Key Decisions Required:**
- Switch platform: Ship or cut? (Decision by Week 47 based on performance data)
- Early Access or full launch? (Decision by Week 50 based on polish level and wishlist count)
- Post-launch content roadmap: Patch schedule locked by Week 52

**Risk Mitigation:**
- **Risk**: Critical bug discovered late (Week 50+)
  - **Mitigation**: QA starts Week 44 (early in Beta). Regression suite catches issues before they compound. Daily builds tested.
- **Risk**: Balance issues surface in final playtests
  - **Mitigation**: Formulas are data-driven (ScriptableObject config). Balance patches deployable post-launch without code changes.
- **Risk**: Switch performance unacceptable (<25fps)
  - **Mitigation**: Decision point Week 47. If perf doesn't hit 30fps, cut Switch platform. Focus on PC launch quality.

### MILESTONE 5: LAUNCH (Month 13, Weeks 53-56)

**Entry Criteria:**
- Beta exit criteria met
- Steam build uploaded and tested
- Press embargo lifted
- Marketing campaign active (2 weeks pre-launch)

**Exit Criteria:**
- ✓ Game live on Steam
- ✓ Launch day support (monitoring for crashes, hotfix deployment ready)
- ✓ Press coverage secured (3+ major outlets: PC Gamer, RPS, Eurogamer)
- ✓ Community channels active (Discord server, subreddit, Twitter)
- ✓ First patch (1.1) prepared for Week 2 post-launch (hotfix + balance tweaks)

**Deliverables:**
1. Steam launch (release date announced 2 weeks prior)
2. Day-one patch ready (any critical bugs from launch day)
3. Press outreach (review keys sent Week -2, embargo lifts launch day)
4. Influencer activation (YouTube/Twitch coverage coordinated for launch week)
5. Community management (Discord moderation, Reddit presence, Twitter engagement)
6. Launch monitoring (crash analytics, Steam reviews, player feedback aggregation)
7. Patch 1.1 deployment (Week 2: balance adjustments, minor bug fixes)

**Risk Mitigation:**
- **Risk**: Game-breaking bug discovered post-launch
  - **Mitigation**: Hotfix deployment pipeline tested during Beta. Rollback plan in place (revert to previous build on Steam).
- **Risk**: Negative launch reception (review bombing, balance complaints)
  - **Mitigation**: Patch 1.1 ready Week 2 with balance adjustments. Community communication plan (transparent dev updates).

### MILESTONE 6: POST-LAUNCH (Months 14-15, Weeks 57-63)

**Exit Criteria:**
- ✓ Patch 1.2 deployed (additional content: 20 new film concepts, 5 new tech nodes)
- ✓ Community feedback addressed (balance tuning, QoL improvements)
- ✓ Sales targets reviewed (10k units in first month is baseline)
- ✓ Post-mortem complete (lessons learned doc)
- ✓ DLC scoping (if sales justify) or project closure decision made

**Deliverables:**
1. Patch 1.2 (additional content + QoL improvements)
2. Community engagement (dev diary posts, AMA on Reddit)
3. Sales data analysis (Steam Analytics review)
4. Player data collection (telemetry: film DNA distributions, box office variance, tech tree paths)
5. Balance tuning (formula adjustments based on real player behavior)
6. Post-mortem doc (what worked, what didn't, what we'd change)
7. DLC scoping doc (if greenlit: "Streaming Wars" expansion extending to 2020)

---

## 3. SPRINT PLAN (DETAILED BREAKDOWN)

### PHASE 1: PROTOTYPE (Weeks 1-12)

**Sprint 1-2 (Weeks 1-2): Foundation**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| Unity project setup (2022.3 LTS, repo, LFS) | BYTE | 8h | None | P0 |
| Git repo + Unity .gitignore config | BYTE | 4h | None | P0 |
| ScriptableObject framework (GameConfig, FilmConcept templates) | BYTE | 12h | None | P0 |
| Data layer structs (Film, FilmDNA, ProductionDecision) | BYTE | 16h | None | P0 |
| EventBus pattern setup | BYTE | 8h | None | P0 |
| Text-based UI shell (main menu, placeholder screens) | BYTE | 8h | None | P0 |
| 5 film concept templates (written, not yet in Unity) | REED | 12h | None | P0 |

**Sprint 3-4 (Weeks 3-4): Film Simulation Core**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| FilmSimulator service (phase progression logic) | BYTE | 24h | Data layer | P0 |
| Film DNA calculation (LockStoryDepthBase method) | BYTE | 16h | FilmSimulator | P0 |
| Decision gate system (ProductionDecision struct, apply logic) | BYTE | 16h | FilmSimulator | P0 |
| Development phase implementation (2-3 quarters, story outline choice) | BYTE | 16h | FilmSimulator | P0 |
| Production phase implementation (animator allocation, crunch) | BYTE | 20h | FilmSimulator | P0 |
| Post-production phase implementation (lighting, score, test screening) | BYTE | 12h | FilmSimulator | P0 |
| Greenlight UI (text-based, show concept cards, select one) | BYTE | 12h | FilmSimulator | P0 |
| 5 additional film concept templates | REED | 12h | None | P1 |

**Sprint 5-6 (Weeks 5-6): Box Office & Reviews**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| BoxOfficeSimulator service (revenue calculation) | BYTE | 20h | Film DNA | P0 |
| Opening weekend formula implementation | BYTE | 12h | BoxOfficeSimulator | P0 |
| Weekly drop-off + WOM calculation | BYTE | 12h | BoxOfficeSimulator | P0 |
| Projector Score calculation | BYTE | 12h | BoxOfficeSimulator | P0 |
| Audience Score calculation | BYTE | 8h | BoxOfficeSimulator | P0 |
| ReviewTemplate ScriptableObject structure | BYTE | 8h | None | P0 |
| ReviewGenerator service (procedural quote generation) | BYTE | 16h | ReviewTemplate | P0 |
| 5 review templates (high score, mid score, low score, spectacle-heavy, heart-heavy) | REED | 16h | None | P0 |
| Box Office Results UI (text-based, display numbers + reviews) | BYTE | 12h | BoxOfficeSimulator | P0 |

**Sprint 7-8 (Weeks 7-8): Save/Load & Integration**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| StudioState root structure | BYTE | 8h | All data layers | P0 |
| SaveSystem service (JSON serialization) | BYTE | 16h | StudioState | P0 |
| Save/load UI (buttons, save slot display) | BYTE | 12h | SaveSystem | P0 |
| Save file versioning + migration logic | BYTE | 12h | SaveSystem | P0 |
| GameLoopController (quarter tick integration) | BYTE | 16h | All services | P0 |
| Production Pipeline Board UI (text-based, show film phases) | BYTE | 12h | FilmSimulator | P0 |
| Unit tests: Film DNA calculation determinism | BYTE | 12h | FilmSimulator | P0 |
| Decision attribution tracking (post-mortem screen) | BYTE | 12h | Film | P0 |

**Sprint 9-10 (Weeks 9-10): Playtest Prep & Refinement**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| Polish text UI (layout, readability, flow) | BYTE | 16h | All UI | P1 |
| Tutorial flow (first greenlight, first decision gate) | BYTE | 12h | UI | P1 |
| Balancing pass: DNA score ranges (playtest and adjust) | REED | 16h | FilmSimulator | P0 |
| Balancing pass: Box office multipliers | REED | 12h | BoxOfficeSimulator | P0 |
| Playtest build preparation (standalone Windows build) | BYTE | 8h | All | P0 |
| Bug fixing (issues from internal testing) | BYTE | 20h | All | P0 |
| 5 playtest sessions (external playtesters, 1 film each) | REED | 20h | Build | P0 |

**Sprint 11-12 (Weeks 11-12): Validation & Handoff**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| Playtest feedback integration (UX tweaks, clarity improvements) | BYTE | 24h | Playtest | P0 |
| Determinism validation (fixed seed, identical outcomes) | BYTE | 8h | All | P0 |
| Save/load stress test (save at each phase, reload, verify) | BYTE | 8h | SaveSystem | P0 |
| Milestone 1 exit criteria validation checklist | BYTE | 8h | All | P0 |
| Prototype retrospective (what worked, what didn't) | Team | 4h | All | P0 |
| Vertical Slice planning (art style lockdown meeting) | Team | 8h | Prototype complete | P0 |

**PROTOTYPE RISKS:**
- **Risk 1**: Core loop takes >30 min per film (target: 15-20 min)
  - Mitigation: Decision density audit Week 8. Cut decisions if flow is slow.
- **Risk 2**: DNA scoring feels random
  - Mitigation: Decision attribution must show clear cause-effect. If playtesters can't explain scores, rework.
- **Risk 3**: Procedural reviews feel generic
  - Mitigation: If reviews don't pass "authored" quality bar Week 10, bring in writer early (originally planned Week 16).

---

### PHASE 2: VERTICAL SLICE (Weeks 13-26)

**Sprint 13-14 (Weeks 13-14): Diegetic UI Foundation**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| Studio View scene (isometric camera, room layout) | PIXEL | 24h | None | P0 |
| Room navigation system (click to enter, camera transitions) | BYTE | 16h | Studio View | P0 |
| Corkboard material/texture (paper, cork, pins) | PIXEL | 16h | None | P0 |
| Greenlight Table UI (diegetic, cards pinned to board) | BYTE + PIXEL | 24h | Corkboard | P0 |
| Film concept card design (layout, iconography) | PIXEL | 12h | None | P0 |
| Pushpin interaction (click to pin/unpin, visual feedback) | BYTE | 12h | Greenlight Table | P0 |
| Studio ambience (HVAC hum, distant sounds) | ECHO | 8h | None | P1 |

**Sprint 15-16 (Weeks 15-16): Production Board**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| Production Pipeline Board design (6 phases, wall-mounted) | PIXEL | 20h | None | P0 |
| Film card design (portrait, progress ring, budget status) | PIXEL | 16h | None | P0 |
| Film card animation (slide between phases) | BYTE | 12h | Production Board | P0 |
| Phase gate decision modal (overlay, decision cards) | BYTE + PIXEL | 24h | Production Board | P0 |
| Decision card layout (narrative text, costs, DNA preview) | PIXEL | 12h | None | P0 |
| Production Board UI implementation | BYTE | 24h | Design | P0 |

**Sprint 17-18 (Weeks 17-18): Talent System**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| Director struct (Vision, Ego, CommercialSense, Specialty) | BYTE | 8h | None | P0 |
| Animator struct (Speed, Quality, Style, Morale) | BYTE | 8h | None | P0 |
| TalentManager service (hire, assign, morale tick, poaching) | BYTE | 32h | Structs | P0 |
| Character portrait style (reference, test portraits) | PIXEL | 16h | None | P0 |
| 20 Director portraits (illustrated) | PIXEL | 40h | Style | P0 |
| 30 Animator portraits (illustrated) | PIXEL | 40h | Style | P0 |
| Talent Agency Board UI (hiring interface) | BYTE + PIXEL | 24h | Portraits | P0 |
| Talent assignment UI (assign Director, assign Animators to film) | BYTE | 16h | TalentManager | P0 |

**Sprint 19-20 (Weeks 19-20): Tech Tree & Economy**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| TechNode ScriptableObject structure | BYTE | 8h | None | P0 |
| 20 tech tree nodes (10 CG, 8 2D, 2 Hybrid) | REED | 20h | None | P0 |
| TechTree service (research, unlock, effects) | BYTE | 24h | TechNode | P0 |
| Tech Tree UI (node graph layout algorithm) | BYTE | 20h | TechTree | P0 |
| Tech node card design (name, description, cost, time, effects) | PIXEL | 12h | None | P0 |
| EconomyCalc service (budget tracking, quarterly costs) | BYTE | 16h | StudioState | P0 |
| Budget dashboard UI (current budget, income, expenses) | BYTE + PIXEL | 16h | EconomyCalc | P0 |
| Bankruptcy/crisis mode (triggered when budget < -$30M) | BYTE | 12h | EconomyCalc | P0 |

**Sprint 21-22 (Weeks 21-22): Rival AI & Screening Room**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| RivalStudio struct (name, reputation, filmography, strategy) | BYTE | 8h | None | P0 |
| RivalAI service (greenlight, release, poaching) | BYTE | 32h | Structs | P0 |
| 2 rival studios initialized (Luminos = Prestige, TitanToon = Commercial) | REED | 8h | RivalAI | P0 |
| Rival release event (competes with player's film) | BYTE | 12h | RivalAI | P0 |
| Screening Room scene (theater aesthetic, projection screen) | PIXEL | 20h | None | P0 |
| Box Office Gauntlet presentation (LED display, numbers animate) | BYTE + PIXEL | 24h | Screening Room | P0 |
| Review display (critic quotes scroll in) | BYTE | 12h | Box Office | P0 |
| Projector/Audience Score badges | PIXEL | 8h | None | P0 |

**Sprint 23-24 (Weeks 23-24): Content & Polish**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| 25 additional film concept templates (total 30) | REED | 40h | None | P0 |
| 5 additional review templates (total 10) | REED | 20h | None | P0 |
| Contract writer review pass (narrative voice validation) | Writer | 40h | Concepts | P0 |
| Render Farm room (monitors, progress bars, teal lighting) | PIXEL | 16h | None | P1 |
| Filmography Shelf room (glass shelf, film boxes) | PIXEL | 16h | None | P1 |
| FMOD integration (setup, basic SFX import) | ECHO | 16h | None | P0 |
| Pushpin SFX (insert, remove, paper rustle) | ECHO | 8h | FMOD | P0 |
| Paper handling SFX (pickup, place, slide) | ECHO | 8h | FMOD | P0 |
| Ambience layers (storyboard room, render farm, lobby) | ECHO | 16h | FMOD | P0 |

**Sprint 25-26 (Weeks 25-26): Integration & Playtest**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| 3-film campaign flow (1995-2003) | BYTE | 16h | All systems | P0 |
| Era event system (basic: quarter triggers) | BYTE | 12h | GameLoop | P1 |
| UI performance profiling (Canvas draw calls, frame rate) | BYTE | 12h | All UI | P0 |
| Canvas batching optimization | BYTE | 16h | Profiling | P0 |
| Bug fixing (integration issues) | BYTE | 24h | All | P0 |
| Playtest build (Windows standalone) | BYTE | 8h | All | P0 |
| 10 playtest sessions (3-film campaign each) | REED | 40h | Build | P0 |
| Feedback integration (UX, clarity, balance) | BYTE | 24h | Playtest | P0 |
| Milestone 2 exit criteria validation | BYTE | 8h | All | P0 |

**VERTICAL SLICE RISKS:**
- **Risk 1**: Diegetic UI hard to navigate
  - Mitigation: Usability test Week 20 (5 new players, no help). If >3 players struggle, add navigation hints.
- **Risk 2**: Procedural content still generic
  - Mitigation: Writer contract Week 16-18. If not improved, increase hand-authored content ratio.
- **Risk 3**: UI performance <60fps on PC
  - Mitigation: Profiling Week 22. If draw calls >80, aggressive canvas separation. Cut particles if needed.

---

### PHASE 3: ALPHA (Weeks 27-43)

**Sprint 27-30 (Weeks 27-30): Content Expansion**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| 70 additional film concepts (total 100) | REED + Writer | 120h | Templates | P0 |
| 15 additional review templates (total 25) | Writer | 60h | Templates | P0 |
| 20 additional tech nodes (total 40: full tree) | REED | 40h | TechNode | P0 |
| 30 additional Director profiles (total 50) | REED | 30h | Director struct | P0 |
| 70 additional Animator profiles (total 100) | REED | 40h | Animator struct | P0 |
| 80 Voice Actor profiles | REED | 40h | VoiceActor struct | P0 |
| Director portrait batch (30 more, total 50) | PIXEL | 60h | Style | P0 |
| Animator portrait batch (70 more, total 100) | PIXEL | 120h | Style | P0 |
| Voice Actor portrait batch (80 new) | PIXEL | 120h | Style | P0 |

**Sprint 31-34 (Weeks 31-34): Systems Completion**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| Studio Soul system (hidden axis, decision tracking) | BYTE | 24h | StudioState | P0 |
| Studio Soul effects (talent attraction, pitch types, review bias) | BYTE | 20h | Studio Soul | P0 |
| Sequel/franchise mechanics (sequel greenlight, fatigue tracking) | BYTE | 24h | FilmSimulator | P0 |
| Awards season system (Best Animated Feature from 2001) | BYTE | 32h | BoxOffice | P0 |
| Oscar ceremony presentation (screening room, envelope, winner reveal) | BYTE + PIXEL | 24h | Awards | P0 |
| Director morale showdown (override consequences, walkout risk) | BYTE | 16h | TalentManager | P0 |
| Test screening system (focus group results, re-cut decisions) | BYTE | 20h | FilmSimulator | P0 |
| Era event system expansion (2D collapse 2003, Oscar 2001, tech milestones) | BYTE | 20h | GameLoop | P0 |
| End-game retrospective (legacy summary, filmography review) | BYTE | 24h | StudioState | P0 |
| Procedural legacy text generation | BYTE | 16h | Retrospective | P0 |

**Sprint 35-38 (Weeks 35-38): Audio & UI Polish**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| SFX library completion (300+ assets) | ECHO | 80h | FMOD | P0 |
| Foley recording session (pushpins, paper, projector, etc.) | ECHO | 24h | None | P0 |
| Environmental recording (computer hums, HVAC, footsteps) | ECHO | 16h | None | P0 |
| Ambience layer implementation (all studio rooms) | ECHO | 32h | FMOD | P0 |
| Adaptive music composition (5 themes, stems) | Composer | 80h | None | P0 |
| Music recording session (piano, strings, woodwinds) | Composer | 40h | Composition | P0 |
| Scripted music cues (6 cues: First Greenlight, Oscar Win, etc.) | Composer | 40h | Composition | P0 |
| FMOD adaptive music implementation | ECHO | 32h | Music stems | P0 |
| UI animation pass (card transitions, count-ups, particles) | BYTE + PIXEL | 40h | All UI | P0 |
| Greenlight stamp animation (hero moment) | PIXEL | 12h | Greenlight | P0 |
| Box office number count-up animation | BYTE | 8h | Box Office | P0 |

**Sprint 39-42 (Weeks 39-42): Integration & Balance**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| Full 60-quarter campaign integration | BYTE | 24h | All systems | P0 |
| Era pacing tuning (event density per era) | REED | 20h | Era events | P0 |
| Box office formula spreadsheet modeling (100 simulated films) | REED | 24h | BoxOffice | P0 |
| Tech tree cost/time balancing (opportunity cost analysis) | REED | 16h | TechTree | P0 |
| Sequel fatigue curve tuning (3rd sequel should be marginal) | REED | 12h | Sequel system | P0 |
| Studio Soul threshold tuning (when do effects trigger?) | REED | 16h | Studio Soul | P0 |
| Awards algorithm validation (10 simulated seasons) | REED | 16h | Awards | P0 |
| Rival AI aggression tuning (competitive but not oppressive) | REED | 12h | RivalAI | P0 |
| 3 full campaign playtests (different strategies: 2D, commercial, prestige) | REED | 120h | Build | P0 |
| Bug fixing (playtest findings) | BYTE | 40h | Playtest | P0 |

**Sprint 43 (Week 43): Validation & Handoff**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| Performance profiling (late-game with 3 films, 50 staff) | BYTE | 12h | All | P0 |
| Quarterly tick amortization (if needed for perf) | BYTE | 16h | Profiling | P1 |
| Save/load stress test (Q60 save, load every quarter) | BYTE | 8h | SaveSystem | P0 |
| Alpha exit criteria validation checklist | BYTE | 8h | All | P0 |
| Alpha retrospective (lessons, risks, Beta scope) | Team | 4h | All | P0 |
| Feature freeze declaration | CLOCK | 1h | All | P0 |

**ALPHA RISKS:**
- **Risk 1**: Mid-campaign sag not addressed
  - Mitigation: Era 3 event density must break routine. If playtest Hour 5-6 feels stale, add more crisis events.
- **Risk 2**: Content authoring behind schedule
  - Mitigation: 100 concepts may reduce to 80 if needed. Quality over quantity. Writer contract extended if required.
- **Risk 3**: Late-game performance <60fps
  - Mitigation: Amortize tick Week 38 if profiling shows >16ms spikes. Accept "Processing..." UI.

---

### PHASE 4: BETA (Weeks 44-52)

**Sprint 44-46 (Weeks 44-46): QA & Bug Fixing**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| QA contractor onboarding | QA Lead | 8h | None | P0 |
| Regression test suite design | QA Lead | 16h | Alpha | P0 |
| Full campaign QA pass (3 complete runs, different strategies) | QA Lead | 120h | Alpha | P0 |
| Edge case testing (bankrupt recovery, all-2D, sequel-only, max crunch) | QA Lead | 60h | Alpha | P0 |
| Save/load stress test (save/load every quarter, 60 quarters) | QA Lead | 40h | Alpha | P0 |
| Bug database setup (Trello or GitHub Issues) | QA Lead | 4h | None | P0 |
| Critical bug fixing (crashes, blockers) | BYTE | 60h | QA findings | P0 |
| Major bug fixing (progression issues, data corruption) | BYTE | 40h | QA findings | P0 |
| Minor bug fixing (UI glitches, typos) | BYTE | 32h | QA findings | P1 |

**Sprint 47-48 (Weeks 47-48): Optimization**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| Profiling full campaign on PC (Unity Profiler deep dive) | BYTE | 16h | Beta build | P0 |
| Canvas batching final pass (target: <50 draw calls) | BYTE | 20h | Profiling | P0 |
| UI animation optimization (reduce simultaneous animators) | BYTE | 12h | Profiling | P0 |
| Quarterly tick optimization (cache calculations, avoid LINQ) | BYTE | 16h | Profiling | P0 |
| Switch build profiling (if platform still viable) | BYTE | 16h | Beta build | P1 |
| Switch performance optimization (if <30fps, aggressive cuts) | BYTE | 24h | Switch profile | P1 |
| Switch platform go/no-go decision | CLOCK | 4h | Switch perf | P0 |
| Save/load async implementation (background thread) | BYTE | 16h | SaveSystem | P1 |
| GZip compression for saves | BYTE | 8h | SaveSystem | P1 |

**Sprint 49-50 (Weeks 49-50): Platform & Steam Integration**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| Windows x64 build (IL2CPP backend) | BYTE | 8h | Beta | P0 |
| macOS build (if time permits) | BYTE | 12h | Beta | P1 |
| Switch build (if platform viable) | BYTE | 16h | Beta | P1 |
| Steamworks integration (SDK setup) | BYTE | 12h | None | P0 |
| Steam achievements (30-40 achievements defined and implemented) | BYTE + REED | 32h | Steamworks | P0 |
| Steam cloud save integration | BYTE | 12h | Steamworks | P0 |
| Steam rich presence (display current quarter, film count) | BYTE | 8h | Steamworks | P0 |
| Steam Input API (controller remapping) | BYTE | 12h | Steamworks | P1 |
| Steam page live (capsule art, screenshots, description) | PIXEL + REED | 24h | None | P0 |
| Trailer production (2 min: diegetic UI showcase, decision moments) | PIXEL + ECHO | 40h | Beta build | P0 |
| Press kit (fact sheet, screenshots, GIFs, press release) | REED | 16h | Trailer | P0 |

**Sprint 51-52 (Weeks 51-52): Final Polish & Launch Prep**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| Final bug sweep (all P1 bugs addressed or deferred to patch) | BYTE | 32h | QA | P0 |
| 5 "blind" playtests (external, no dev contact, full campaign) | REED | 60h | Beta build | P0 |
| Blind playtest feedback integration | BYTE | 24h | Blind tests | P0 |
| Balance data analysis (player telemetry from blind tests) | REED | 16h | Blind tests | P0 |
| Patch 1.1 prep (balance adjustments, hotfix bugs) | BYTE | 24h | Data | P0 |
| Localization string table externalization (for future loc) | BYTE | 16h | All | P1 |
| Early Access vs. full launch decision | CLOCK | 4h | Beta state | P0 |
| Launch date announcement (2 weeks before launch) | CLOCK | 4h | Decision | P0 |
| Press embargo coordination (review keys, NDA, embargo date) | REED | 12h | Press kit | P0 |
| Influencer key distribution (50 keys, coordinated coverage) | REED | 12h | Launch date | P0 |
| Community channel setup (Discord server, subreddit, Twitter) | REED | 16h | None | P0 |
| Beta exit criteria validation checklist | BYTE | 8h | All | P0 |

**BETA RISKS:**
- **Risk 1**: Critical bug discovered Week 50+
  - Mitigation: Daily QA builds from Week 44. Catch issues early. If critical bug Week 51, delay launch 1 week (acceptable).
- **Risk 2**: Balance issues in final playtests
  - Mitigation: Formulas are data-driven. Patch 1.1 ready Week 2 post-launch with adjustments.
- **Risk 3**: Switch performance unacceptable
  - Mitigation: Go/no-go Week 47. If cut, focus all effort on PC quality. Announce as PC-exclusive.

---

### PHASE 5: LAUNCH (Weeks 53-56)

**Sprint 53 (Week 53): Launch Week**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| Steam build upload (production branch) | BYTE | 8h | Beta complete | P0 |
| Steam build verification (download, test on clean machine) | BYTE | 4h | Upload | P0 |
| Launch day monitoring setup (crash analytics, Steam stats) | BYTE | 8h | None | P0 |
| Press embargo lifts (reviews go live) | REED | 4h | Launch | P0 |
| Social media launch posts (Twitter, Discord, Reddit) | REED | 4h | Launch | P0 |
| Community management (Discord moderation, Reddit responses) | REED | 20h/week | Launch | P0 |
| Hotfix deployment (if critical bugs surface) | BYTE | 40h | Launch | P0 |
| Player feedback aggregation (Steam reviews, Discord, Reddit) | REED | 16h | Launch | P0 |

**Sprint 54-56 (Weeks 54-56): Post-Launch Support**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| Patch 1.1 deployment (balance tweaks, minor bug fixes) | BYTE | 32h | Feedback | P0 |
| Patch 1.1 release notes | REED | 4h | Patch | P0 |
| Community engagement (dev diary post, Reddit AMA) | REED | 12h | Launch | P0 |
| Sales data review (Steam Analytics) | CLOCK | 8h | Week 2 | P0 |
| Player data collection (telemetry: DNA distributions, box office variance) | BYTE | 16h | Launch | P1 |
| Balance tuning analysis (formula adjustments for Patch 1.2) | REED | 20h | Data | P1 |
| Crash triage (fix any new crashes reported) | BYTE | 24h | Launch | P0 |
| Press follow-up (thank reviewers, respond to coverage) | REED | 8h | Launch | P0 |

**LAUNCH RISKS:**
- **Risk 1**: Game-breaking bug discovered post-launch
  - Mitigation: Hotfix pipeline tested. Rollback plan ready. 24-hour response time.
- **Risk 2**: Negative review wave (balance complaints, "unfair" box office)
  - Mitigation: Patch 1.1 Week 2 with balance adjustments. Transparent communication on Discord/Twitter.
- **Risk 3**: Sales miss baseline (10k units Month 1)
  - Mitigation: Marketing spend increase (influencer activation, Steam sale consideration). Not a project-killer, but informs DLC decision.

---

### PHASE 6: POST-LAUNCH (Weeks 57-63)

**Sprint 57-60 (Weeks 57-60): Patch 1.2 & Content**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| 20 new film concept templates | REED | 40h | Patch 1.1 | P1 |
| 5 new tech tree nodes | REED | 20h | Patch 1.1 | P1 |
| QoL improvements (UI shortcuts, tooltips, filters) | BYTE | 32h | Feedback | P1 |
| Balance formula adjustments (data-driven from player behavior) | REED | 24h | Data | P0 |
| Patch 1.2 QA pass | QA Lead | 40h | Patch | P1 |
| Patch 1.2 deployment | BYTE | 16h | QA | P1 |
| Patch 1.2 release notes (changelog, new content highlight) | REED | 4h | Patch | P1 |
| Community update (dev diary: what's next) | REED | 8h | Patch | P1 |

**Sprint 61-63 (Weeks 61-63): Post-Mortem & Future Planning**
| Task | Owner | Est. | Dependency | Priority |
|------|-------|------|------------|----------|
| Post-mortem document (what worked, what didn't, lessons learned) | Team | 16h | Patch 1.2 | P0 |
| Sales data final review (first 2 months) | CLOCK | 8h | Sales data | P0 |
| Player data analysis deep dive (what strategies are popular?) | REED | 20h | Telemetry | P1 |
| DLC scoping (if sales justify: "Streaming Wars" expansion 2020) | Team | 16h | Sales review | P1 |
| DLC pitch doc (if greenlit) | REED | 24h | Scoping | P1 |
| Project closure decision (DLC or sunset) | CLOCK | 4h | DLC scope | P0 |
| Archive project (repo, builds, docs, post-mortem) | BYTE | 8h | Closure | P0 |

**POST-LAUNCH SUCCESS CRITERIA:**
- 10,000 units sold Month 1 (baseline)
- "Very Positive" Steam review rating (80%+ positive)
- Active community (Discord 500+ members, subreddit 1k+ subs)
- Player data shows diverse strategies (not just one dominant path)

---

## 4. RISK REGISTER

### 4.1 High-Impact, High-Likelihood Risks

**RISK 1: Procedural Content Feels Algorithmic**
- **Likelihood**: Medium (40%)
- **Impact**: High (kills emotional investment)
- **Mitigation**:
  - Writer-authored templates, not programmer-generated
  - 30+ hour playtests to surface repetition
  - Fallback: reduce procedural ratio, increase hand-authored content
  - Decision point: Week 26 (Vertical Slice exit). If not resolved, bring in additional writer.
- **Contingency**: If procedural generation fails quality bar, pivot to 60-80 hand-authored film concepts (no templates). Scope cut, but preserves quality.
- **Owner**: REED

**RISK 2: Mid-Campaign Sag (Hours 4-7)**
- **Likelihood**: Medium (35%)
- **Impact**: High (player drops off before endgame)
- **Mitigation**:
  - Era 3 events designed for disruption (2D collapse, rival mega-hit, studio crisis)
  - Playtest pacing instrumentation (log alt-tabs, time skips, boredom signals)
  - Decision point: Week 40 (Alpha playtest 2). If sag detected, increase event density.
- **Contingency**: Add "Crisis Mode" event that forces player adaptation (mandatory layoffs, forced tech pivot). Breaks routine mechanically.
- **Owner**: REED

**RISK 3: UI Performance on Switch <30fps**
- **Likelihood**: Medium (35%)
- **Impact**: Medium (lose secondary platform, but PC is primary)
- **Mitigation**:
  - Profile on Switch devkit Week 20 (early Vertical Slice)
  - Aggressive canvas batching, particle reduction
  - Go/no-go decision Week 47
- **Contingency**: Cut Switch platform. Focus all effort on PC quality. Announce as PC-exclusive at launch. Revisit Switch post-launch if sales justify optimization effort.
- **Owner**: BYTE

### 4.2 Medium-Impact, Medium-Likelihood Risks

**RISK 4: Box Office Formula Imbalanced**
- **Likelihood**: Medium (40%)
- **Impact**: Medium (fixable post-launch via patch)
- **Mitigation**:
  - Spreadsheet modeling (100 simulated films, Week 35)
  - Playtest data collection (all film releases logged with DNA + outcomes)
  - Balance patch post-launch if needed
- **Contingency**: Patch 1.1 (Week 2 post-launch) includes formula adjustments. If major rebalance needed, communicate transparently to community.
- **Owner**: REED

**RISK 5: Save File Corruption**
- **Likelihood**: Low (15%)
- **Impact**: High (player trust killer)
- **Mitigation**:
  - Atomic save writes (temp file → rename)
  - Versioned format with migration
  - Extensive QA (save/load every quarter for 60 quarters)
  - Backup autosaves (keep last 3)
- **Contingency**: If corruption reported, emergency hotfix. Offer affected players direct support (restore from backup or compensation).
- **Owner**: BYTE

**RISK 6: Rival AI Too Weak or Too Strong**
- **Likelihood**: Medium (30%)
- **Impact**: Medium (tunable post-launch)
- **Mitigation**:
  - Difficulty settings (Easy/Normal/Hard)
  - Playtest with varied skill levels
  - Rival aggression tuning Week 38
- **Contingency**: Patch 1.1 includes difficulty rebalancing based on player feedback. Default to "Normal" at launch.
- **Owner**: REED

### 4.3 Low-Impact or Low-Likelihood Risks

**RISK 7: Talent Portraits Feel Inconsistent**
- **Likelihood**: Low (20%)
- **Impact**: Low (cosmetic, not gameplay)
- **Mitigation**: Style guide enforced from first portrait batch (Week 17)
- **Contingency**: Art revision pass Week 30 if needed. Not a launch blocker.
- **Owner**: PIXEL

**RISK 8: Music Doesn't Fit Tone**
- **Likelihood**: Low (15%)
- **Impact**: Medium (audio is 50% of feel)
- **Mitigation**: Composer briefed with tone references (Whiplash, Social Network, Up). Early demo (Week 32) for approval.
- **Contingency**: If music doesn't fit, license stock tracks as fallback. Not ideal, but shippable.
- **Owner**: ECHO

**RISK 9: Steam Review Bombing**
- **Likelihood**: Low (10%)
- **Impact**: Medium (hurts sales)
- **Mitigation**: Community management, rapid response to legitimate complaints, patch schedule
- **Contingency**: Transparent dev communication, Patch 1.1 addresses top complaints
- **Owner**: REED

---

## 5. CRITICAL PATH

The critical path is the longest dependency chain that determines minimum project duration. Any delay here delays the ship date.

**CRITICAL PATH SEQUENCE:**

```
Prototype Core Loop (Weeks 1-12)
    |
    v
Vertical Slice (Weeks 13-26)
    |
    v
Content Authoring (Weeks 27-30, parallel with Systems Completion)
    |
    v
Alpha Integration (Weeks 31-42)
    |
    v
QA & Bug Fixing (Weeks 44-48)
    |
    v
Final Polish (Weeks 49-52)
    |
    v
Launch (Week 53)
```

**CRITICAL PATH TASKS (No Slack):**

1. **FilmSimulator Implementation** (Weeks 3-6): Everything depends on this. Delay here cascades.
2. **Diegetic UI Foundation** (Weeks 13-16): UI is identity. Delay risks entire Vertical Slice milestone.
3. **Content Authoring** (Weeks 27-30): 100 concepts + 25 reviews is large scope. Delays here push Alpha exit.
4. **Full Campaign Integration** (Week 39): Merging all systems. High bug risk. Delay here compresses Beta.
5. **QA Pass** (Weeks 44-48): Cannot ship without QA. Delay here delays launch.

**SLACK IN SCHEDULE (Tasks That Can Absorb Delay):**

- Audio implementation (Weeks 23-38): ECHO can start later or extend if needed. Not on critical path until Week 38 (Alpha exit).
- Portrait creation (Weeks 17-30): PIXEL can batch portraits across longer timeframe if needed. Placeholder portraits work for playtests.
- Tech Tree expansion (Weeks 27-30): Can ship with 30 nodes instead of 40 if needed. Not critical path.
- Post-launch content (Weeks 57-63): Entirely off critical path for v1.0 launch.

**DECISION POINTS ON CRITICAL PATH:**

| Week | Decision | Impact If Delayed |
|------|----------|-------------------|
| 8 | Core loop validation (playtest) | 2-week delay cascades to Vertical Slice |
| 26 | Vertical Slice exit criteria met? | 2-week delay cascades to Alpha |
| 40 | Alpha systems complete? | 1-week delay per incomplete system |
| 47 | Switch go/no-go | If cut, saves 2 weeks (optimization time freed) |
| 52 | Beta exit criteria met? | Delay launch date (1 week delay acceptable, 2+ weeks risky) |

**MITIGATION FOR CRITICAL PATH RISKS:**

1. **Weekly Status Check**: Every Monday, review critical path tasks. Flag delays immediately.
2. **Scope Cut Authority**: CLOCK has authority to cut non-critical features if critical path is at risk.
3. **Crunch Avoidance**: Build 2-week buffer into Beta (Weeks 51-52 are "polish and contingency"). Avoid crunch by cutting scope, not padding schedule.
4. **Parallel Work**: Maximize parallel work where dependencies allow. Example: Audio and portraits can progress while FilmSimulator is being built.

---

## 6. SCOPE MANAGEMENT

### 6.1 Scope Control Process

**Feature Freeze: End of Week 43 (Alpha Exit)**

After Alpha exit, no new features. Only bug fixes, balance tuning, and polish.

**Change Request Process (Pre-Freeze):**

1. Feature request submitted to CLOCK (any team member can submit)
2. CLOCK evaluates:
   - Does this serve core player fantasy? (Creative stewardship of studio)
   - Does this fit in remaining schedule without delaying milestones?
   - Does this require new systems or extend existing systems?
3. CLOCK approves, defers to post-launch, or rejects
4. If approved, task added to sprint and critical path re-evaluated

**Post-Freeze Change Process:**

1. Only critical bugs and balance issues addressed
2. Any feature requests logged for Patch 1.2 or DLC
3. Exception: If a "must-have for launch" feature is discovered (e.g., players universally confused by a UI element), CLOCK can approve if:
   - Fix is <16 hours of work
   - Does not add new systems
   - Does not delay launch

### 6.2 What's In, What's Cut, What's At Risk

**LOCKED IN (Non-Negotiable for v1.0):**
- Film Production Pipeline (6 phases)
- Diegetic Studio Interface
- Film DNA System (8 attributes)
- Talent Engine (4 types)
- Technology Tree (40 nodes)
- Box Office Gauntlet
- Rival Studio AI (3 rivals)
- Era Simulation (1995-2010)
- Save/Load
- Full 60-quarter campaign
- End-game retrospective

**CUT FROM v1.0 (Deferred to Post-Launch or DLC):**
- Studio Culture System (crunch detail, workplace health)
- Sequel Machine (advanced franchise management)
- Press Tour mini-game
- Director's Cut mode
- Industry Events (procedural disruptions beyond era events)
- Modding support
- Localization (English only at launch)

**AT RISK (May Cut If Schedule Slips):**
- Nintendo Switch platform (go/no-go Week 47)
- macOS build (secondary to Windows)
- 100 film concepts (fallback: 80 concepts)
- Render Farm room visuals (can be simplified if art bandwidth tight)
- Filmography Shelf room visuals (can be text-based UI fallback)
- Voice Actor portraits (fallback: generic icons instead of illustrated portraits)

### 6.3 Scope Escalation (When Things Go Wrong)

**If 1 Week Behind Schedule:**
- Cut at-risk features (macOS, some portraits)
- Increase parallel work (add contractor hours)
- Minor crunch (team works 45h/week instead of 40h for 2 weeks max)

**If 2 Weeks Behind Schedule:**
- Cut Switch platform
- Reduce film concepts to 80
- Cut Filmography Shelf room (text UI instead)
- Voice Actor portraits become generic icons
- Team works 45h/week for 4 weeks

**If 3+ Weeks Behind Schedule:**
- Consider Early Access launch instead of full launch
- Ship with 50-60 film concepts (still playable, less variety)
- Cut all secondary platforms (PC Windows only)
- Simplify rival AI (2 rivals instead of 3)
- Delay launch date 4 weeks (announce publicly, transparent communication)

**Scope Cut Authority Hierarchy:**
1. At-risk features: CLOCK can cut without team vote
2. Locked-in features: Requires team consensus to cut
3. Core player fantasy features: Cannot cut (project fails without these)

---

## 7. BUDGET BREAKDOWN

### 7.1 Personnel Costs (15 Months)

**Core Team:**
- BYTE (Lead Programmer): $120k/year × 1.25 years = $150k
- PIXEL (Art Director): $90k/year × 1.0 years = $90k
- ECHO (Sound Designer): $75k/year × 0.75 years = $56k
- REED (Lead Designer): $100k/year × 0.625 years (0.5 FTE × 1.25 years) = $63k

**Subtotal Core**: $359k

Wait, that's over budget. Let me recalculate for indie/contractor rates.

**Revised Core Team (Indie Rates):**
- BYTE: $80k contract (15 months, full-time)
- PIXEL: $60k contract (12 months, full-time)
- ECHO: $28k contract (9 months, half-time)
- REED: $40k contract (15 months, half-time)

**Subtotal Core**: $208k

**Contractors:**
- Composer: 200 hours × $60/hr = $12k
- Writer: 150 hours × $60/hr = $9k
- QA Lead: 320 hours × $50/hr = $16k
- Playtester Pool: 160 sessions × $50/session = $8k

**Subtotal Contractors**: $45k

**Total Personnel**: $253k

### 7.2 Tools & Services (15 Months)

**Software Licenses:**
- Unity Pro (4 seats): $150/mo × 15 × 4 = $9k
- Adobe Creative Cloud (PIXEL): $55/mo × 12 = $660
- FMOD Studio (indie license): Free
- GitHub (private repo, LFS): $4/mo × 15 = $60

**Subtotal Software**: $9,720

**Hardware:**
- Switch devkit (if pursuing platform): $500 (Nintendo provides to licensed devs)
- Mid-tier PC for testing (integrated graphics): $800

**Subtotal Hardware**: $1,300

**Services:**
- Cloud storage (Google Drive for builds/assets): $10/mo × 15 = $150
- Steam Direct fee: $100
- Web hosting (press kit site): $10/mo × 15 = $150

**Subtotal Services**: $400

**Total Tools & Services**: $11,420

### 7.3 Marketing & Launch

**Pre-Launch:**
- Trailer production (contractor if not in-house): $2k (if PIXEL + ECHO produce in-house, $0)
- Key art / capsule images: In-house (PIXEL)
- Press kit: In-house (REED)

**Subtotal Pre-Launch**: $2k (or $0 if in-house)

**Post-Launch:**
- Influencer keys (50 keys, free but opportunity cost)
- Paid ads (Steam Discovery Queue, Twitter): $5k (optional, only if sales justify)
- Community management tools (Discord Nitro, Reddit ads): $300

**Subtotal Post-Launch**: $5,300 (or $300 if no paid ads)

**Total Marketing**: $7,300 (conservative estimate)

### 7.4 Contingency & Miscellaneous

**Contingency** (10% of personnel + tools): $26,500
**Miscellaneous** (conferences, travel, legal): $5,000

**Total Contingency & Misc**: $31,500

### 7.5 Total Budget

| Category | Amount |
|----------|--------|
| Personnel (Core) | $208,000 |
| Personnel (Contractors) | $45,000 |
| Tools & Services | $11,420 |
| Marketing | $7,300 |
| Contingency & Misc | $31,500 |
| **TOTAL** | **$303,220** |

**Budget Range**: $280k-$320k depending on marketing spend and contingency usage.

**Funding Sources** (Indie Scenario):
- Personal savings / founder investment: $100k
- Angel investor / friends & family: $100k
- Kickstarter / crowdfunding: $50k
- Publisher advance / grant: $50k-$100k

OR:

**Bootstrapped Scenario** (Lower Budget):
- Cut core team salaries (deferred compensation or equity)
- Self-funded ($50k personal investment)
- Scope reduced (80 concepts instead of 100, cut Switch, no paid marketing)
- **Total**: $150k-$180k

---

## 8. DEPENDENCIES

### 8.1 External Dependencies

**Unity Engine:**
- Unity 2022.3 LTS (stable release)
- Risk: Unity introduces breaking changes
- Mitigation: LTS version, no mid-project upgrades

**FMOD:**
- FMOD Studio indie license
- Risk: FMOD API changes
- Mitigation: Lock FMOD version, don't upgrade mid-project

**Steamworks SDK:**
- Required for Steam integration (achievements, cloud save)
- Risk: Steamworks API changes
- Mitigation: Unity Steamworks.NET plugin (stable, well-maintained)

**Nintendo Switch SDK** (if platform pursued):
- Requires Nintendo developer license (approved developer status)
- Risk: Approval delay, devkit availability
- Mitigation: Apply for license Week 1. Devkit ships Week 8-12.

**Asset Store / Third-Party Plugins:**
- DOTween (UI animation)
- TextMesh Pro (included in Unity)
- Risk: Plugin incompatibility, deprecation
- Mitigation: Use widely-adopted, actively-maintained plugins

### 8.2 Internal Dependencies (Task Dependencies)

**Blocking Dependencies:**

| Task | Blocked By | Unblocks |
|------|------------|----------|
| Film DNA Calculation | FilmSimulator | Box Office Calculation, Review Generation |
| Box Office UI | Box Office Calculation | Playtest (Prototype) |
| Talent Assignment UI | TalentManager | Film Production Integration |
| Tech Tree UI | TechTree Service | Tech Effects Application |
| Diegetic Studio View | Studio Art | All Room UIs |
| Adaptive Music | Music Stems | FMOD Integration |
| Full Campaign | All Core Systems | QA, Beta |

**Parallelizable Work (No Dependencies):**

- Portrait creation (Weeks 17-30) — parallel with systems work
- Audio asset creation (Weeks 23-38) — parallel with UI development
- Content authoring (Weeks 27-30) — parallel with systems completion
- Marketing materials (Weeks 49-52) — parallel with final polish

### 8.3 Team Dependencies

**BYTE-Blocked Tasks** (Critical Path):
- All simulation systems
- Save/load
- UI implementation (code side)
- Performance optimization

**PIXEL-Blocked Tasks**:
- Diegetic UI art
- Character portraits
- Iconography

**ECHO-Blocked Tasks**:
- SFX library
- FMOD integration
- Ambience design

**REED-Blocked Tasks**:
- Content authoring (film concepts, reviews, tech nodes)
- Balance tuning
- Playtesting coordination

**Mitigation for Blocked Work**:
- BYTE is critical path bottleneck. BYTE's tasks are highest priority.
- If BYTE is blocked, team can work on parallel tracks (art, audio, content).
- If BYTE falls behind, consider bringing in contract programmer for specific tasks (e.g., UI implementation, tool scripting).

---

## 9. TEAM COMMUNICATION & WORKFLOW

### 9.1 Meeting Cadence

**Daily Standup** (15 minutes, async on Discord):
- What I did yesterday
- What I'm doing today
- Any blockers

**Weekly Sprint Planning** (Monday, 1 hour):
- Review last week's tasks
- Assign this week's tasks
- Review critical path status

**Bi-Weekly Playtest Review** (Every other Thursday, 2 hours):
- Play latest build together
- Discuss what's working / not working
- Make design decisions based on feel

**Monthly Milestone Review** (Last Friday of month, 2 hours):
- Review milestone exit criteria
- Assess risks
- Adjust schedule if needed

### 9.2 Tools

**Communication:**
- Discord (daily standup, quick questions)
- Zoom (weekly meetings, playtest reviews)

**Task Management:**
- Trello (sprint boards, task assignments)
- Columns: Backlog, This Sprint, In Progress, Testing, Done

**Version Control:**
- Git + GitHub (code, Unity project)
- Git LFS (binary assets)

**Documentation:**
- Google Docs (design docs, meeting notes)
- Confluence (if team prefers wiki format)

**Builds:**
- Unity Cloud Build (automated builds on commit)
- Dropbox (build distribution to playtesters)

### 9.3 Decision-Making Process

**Design Decisions:**
- REED proposes
- Team discusses (async on Discord or sync in meeting)
- REED makes final call (unless impacts schedule)

**Scope Decisions:**
- CLOCK proposes cut
- Team discusses impact
- CLOCK makes final call

**Technical Decisions:**
- BYTE proposes
- Team discusses (especially if impacts design or art)
- BYTE makes final call

**Art Direction Decisions:**
- PIXEL proposes
- Team reviews
- PIXEL makes final call

**Escalation:**
- If team cannot reach consensus, CLOCK breaks tie
- If decision impacts schedule or budget, CLOCK has final authority

---

## 10. DEFINITION OF DONE

### 10.1 Task-Level Done

A task is "done" when:
- Code compiles, no errors
- Functionality works as specified
- No known critical bugs
- Code reviewed by one other team member (if code task)
- Unit tests pass (if applicable)
- Checked into main branch

### 10.2 Feature-Level Done

A feature is "done" when:
- All tasks complete
- Feature integrated with rest of game
- Playtested by at least 2 people (one external to feature owner)
- No blocking bugs
- Performance acceptable (no frame drops)
- Documented (code comments, design doc updated)

### 10.3 Milestone-Level Done

A milestone is "done" when:
- All exit criteria met (see Section 2)
- No critical bugs (P0 bugs = 0)
- Playtest validation complete
- Demo build shippable to external playtesters
- Retrospective complete (lessons learned logged)

---

## 11. FINAL REALITY CHECK

### 11.1 What Could Still Kill This Project

**After all this planning, here's what I'm still worried about:**

1. **Team Burnout**: 15 months is long. If morale drops, quality drops. Mitigation: No crunch. 2-week vacations encouraged. Scope cuts over team health.

2. **Procedural Content Failure**: If film concepts feel generic at Week 26, we're in trouble. We've planned for it (writer contract, fallback to hand-authored), but it's still a risk.

3. **The Game Isn't Fun**: All the systems can work perfectly and the game can still be boring. Playtesting is our canary in the coal mine. If playtesters aren't engaged by Week 20, we have a core loop problem.

4. **Market Timing**: If a competitor ships a similar game during our development, we lose first-mover advantage. Mitigation: Monitor space (Sim gaming Reddit, Steam tags), but ultimately accept risk.

### 11.2 What I'm Confident About

1. **The Team Knows What They're Building**: This isn't vaporware. Every doc (pitch, GDD, narrative, art, sound, tech) is complete. Scope is locked.

2. **The Tech Is Proven**: Unity for management sims is standard. No experimental tech. Low technical risk.

3. **The Schedule Has Slack**: 15 months with 2-week buffer in Beta. Feature freeze at Week 43 gives 9 weeks of polish/QA.

4. **The Scope Can Flex**: We've identified what's cuttable. Switch, macOS, extra content, secondary features — all can be shed to hit launch date.

5. **The Market Exists**: Game Dev Tycoon sold 2M+ copies. Two Point Hospital sold 1M+ in Year 1. Management sims on Steam have proven audience.

### 11.3 Success Metrics (What "Good" Looks Like)

**Month 1 Post-Launch:**
- 10,000 units sold (baseline)
- 75%+ positive Steam reviews
- 3+ major press outlets covered (PC Gamer, RPS, Eurogamer)
- Active community (500+ Discord members, 1k+ subreddit subs)

**Month 6 Post-Launch:**
- 25,000 units sold
- "Very Positive" Steam rating maintained
- Patch 1.2 deployed with additional content
- DLC greenlit (if sales support)

**Month 12 Post-Launch:**
- 50,000+ units sold
- Break-even on $300k budget ($300k revenue at $15 price point = 20k units, accounting for Steam 30% cut)
- Profitability achieved
- Team can sustain for next project

---

## 12. SIGN-OFF

This production plan is locked as of 2026-02-07.

**Scope**: Locked. Feature freeze Week 43.
**Schedule**: 15 months (63 weeks). Launch Week 53.
**Budget**: $280k-$320k. Contingency: $31.5k.
**Team**: 4 core + 4 contractors.

**Approval:**
- CLOCK (Producer): Approved
- BYTE (Lead Programmer): Approved
- PIXEL (Art Director): Approved
- ECHO (Sound Designer): Approved
- REED (Lead Designer): Approved

**Next Steps:**
1. Team kickoff meeting (Week 1, Monday)
2. Unity project initialization (Week 1, Day 1)
3. Sprint 1-2 tasks assigned (Week 1, Day 2)
4. Prototype Milestone begins

Cut scope, not corners. Ship the game.

---

**END OF PRODUCTION PLAN**

**Document Location**: `/Users/burcukose/git/project-draft/games/12-framewar/production-plan.md`

**Related Documents**:
- `/Users/burcukose/git/project-draft/games/12-framewar/pitch.md`
- `/Users/burcukose/git/project-draft/games/12-framewar/game-design.md`
- `/Users/burcukose/git/project-draft/games/12-framewar/narrative-bible.md`
- `/Users/burcukose/git/project-draft/games/12-framewar/art-direction.md`
- `/Users/burcukose/git/project-draft/games/12-framewar/sound-design.md`
- `/Users/burcukose/git/project-draft/games/12-framewar/technical-architecture.md`
