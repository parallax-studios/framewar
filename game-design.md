# FRAMEWAR -- Game Design Document

**Designer**: REED
**Version**: 1.0
**Date**: 2026-02-07
**Status**: Complete First Pass

---

## 1. PLAYER FANTASY STATEMENT

**"I am the head of an animation studio during the most volatile fifteen years in the history of the medium. I greenlight films that take years to make and seconds to judge. I hire brilliant, difficult people and bet my studio's survival on their vision. I decide whether to chase the technology revolution or defend a dying art form. My filmography is my legacy -- and every title on that shelf is a scar or a trophy."**

What's the loop? The player wants to feel like a creative executive -- not a spreadsheet optimizer, not a passive observer, but a person who sits in a screening room at midnight watching a rough animatic and has to decide: is this extraordinary, or is this a disaster I need to kill before it kills my studio? The fantasy is authorship through stewardship. You never draw a frame. You never write a line of dialogue. But every film on your shelf exists because of a chain of decisions only you could have made.

The emotional register shifts across the campaign. Early game: wonder and possibility. Mid game: ambition and pressure. Late game: reckoning and legacy. The player who finishes FRAMEWAR should feel like they lived a career.

---

## 2. CORE LOOP

### 2.1 The 30-Second Loop (Micro-Decision)

Navigate the studio floor. Check active productions. A decision surfaces: approve a storyboard revision, resolve a personnel conflict, allocate render farm hours, review a voice audition tape. Each micro-decision takes 5-15 seconds and adjusts a Film DNA attribute by a small increment (typically +/- 0.2 to 0.5 on a 10-point scale). The player's verb is **JUDGE** -- evaluate, approve, reject, redirect.

Feedback is immediate and diegetic. Approve a shot and you see it pinned to the production board with a green thumbtack. Reject it and it goes back with a red mark. The storyboard room fills up over time -- you can see a film taking shape on the wall.

### 2.2 The 5-Minute Loop (Quarter Management)

Each in-game quarter (roughly 2-3 minutes of real time at default speed), the player manages their active slate. The verbs are **ALLOCATE** and **DECIDE**. Allocate finite studio resources (animators, render farm cycles, story room hours, budget) across 1-3 active productions. Decide on incoming events: a rival announces a competing film, a director wants more time on Act 2, a voice actor's schedule conflicts with your recording window, a technology breakthrough completes and can be applied to an in-progress film.

The quarter ends with a status update: each film advances through its pipeline phase (or stalls if under-resourced). Progress is visible on the Production Pipeline Board.

### 2.3 The Meta Loop (Film Cycle)

A single film's lifecycle -- greenlight to box office aftermath -- takes roughly 20-40 minutes of real time (12-16 in-game quarters, representing 3-4 in-game years). The verbs are **GREENLIGHT**, **SHEPHERD**, and **HARVEST**. Greenlight a concept at the table. Shepherd it through six production phases, making key decisions at each gate. Harvest the results: box office revenue, critical reception, awards, reputation shifts, and talent loyalty changes.

After the harvest, the player surveys their updated studio state -- new budget, shifted reputation, changed talent roster -- and greenlights the next film. The cycle repeats 6-10 times across the full campaign.

### 2.4 Core Loop Diagram

```
                    GREENLIGHT TABLE
                    (Select concept, assign director,
                     set budget, choose tech approach)
                           |
                           v
    +----------------------------------------------+
    |          PRODUCTION PIPELINE                  |
    |  DEV -> PRE-PROD -> PROD -> POST -> MKT -> REL |
    |  (3-5 key decisions per phase)                |
    |  (resources allocated per quarter)            |
    +----------------------------------------------+
                           |
                           v
                   BOX OFFICE GAUNTLET
                   (4-week run, reviews, WOM,
                    awards season)
                           |
                           v
                   HARVEST & RECKONING
                   (Revenue -> Budget pool)
                   (Reviews -> Reputation shift)
                   (Awards -> Talent magnetism)
                   (Film -> Filmography shelf)
                           |
              +------------+------------+
              |                         |
              v                         v
      TALENT ENGINE              TECH TREE
      (Hire/retain/lose          (Invest R&D,
       based on reputation        unlock capabilities,
       and budget)                advance render tech)
              |                         |
              +------------+------------+
                           |
                           v
                    GREENLIGHT TABLE
                    (cycle repeats with
                     new studio state)
```

How does this feel at hour 20? By hour 20, the player is managing their third or fourth simultaneous production, timing releases to avoid rival competition, and juggling a roster of directors and animators with personal agendas. The loop has deepened from "approve shots" to "orchestrate a multi-year studio strategy." The 30-second decisions haven't changed mechanically, but their weight has increased because the player now understands the downstream consequences.

---

## 3. CORE MECHANICS

### 3.1 The Greenlight Table

**Player verb**: EVALUATE and COMMIT.

**System description**: The Greenlight Table is a physical corkboard in the studio's main office. Film pitches arrive as concept cards -- pinned documents with visible and hidden attributes. The player sees:

- **Concept Title and Logline**: "DEEP DARK -- A blind deep-sea fish discovers the surface world." Procedurally generated from a pool of 100+ authored templates with variable elements (protagonist type, setting, central conflict, emotional core).
- **Visible Attributes** (rated 1-10):
  - CONCEPT ORIGINALITY: How fresh is this idea? (Affects ORIGINALITY DNA score)
  - AUDIENCE BREADTH: How wide is the potential audience? (Affects opening weekend multiplier)
  - TECHNICAL AMBITION: How hard is this to make? (Affects production cost and ANIMATION QUALITY ceiling)
  - SEQUEL POTENTIAL: Can this become a franchise? (Affects long-term revenue planning)
- **Hidden Risks**: Each concept has 1-3 hidden risk tags revealed during production. Examples: "Third Act Problem" (STORY DEPTH capped at 7 unless addressed in Development), "Casting Dependent" (VOICE CAST APPEAL has 2x normal weight on box office), "Tone Trap" (HUMOR and HEART inversely correlated for this film -- pushing one suppresses the other).

**Greenlight decisions**: When greenlighting, the player assigns:
1. **Director** (from available roster -- each director has vision traits that bias Film DNA outcomes)
2. **Target Budget**: $40M to $180M in $10M increments. Higher budget = more resource capacity per quarter, higher break-even point.
3. **Release Window**: Target quarter/year. Locking this early gives marketing bonuses (+15% awareness). Moving it later incurs audience skepticism penalty (-5% opening weekend per delay).
4. **Technology Approach**: 2D Traditional, Early CG, Cutting-Edge CG, or Hybrid. Determines which tech tree nodes apply, which animators are eligible, and the film's baseline ANIMATION QUALITY floor/ceiling.

**Depth**: The beginner greenlights based on cool loglines. The expert reads hidden risk probability (certain concept templates have higher variance), matches director vision traits to concept needs, budgets based on pipeline capacity (not just "how much can I spend"), and times release windows against predicted rival releases and awards season calendars. A master-level play is greenlighting a mid-budget "awards bait" film timed for Q4 of an Oscar year with a prestige director, while your tentpole carries the revenue load in summer.

**Constraints**: Maximum 3 films in active production simultaneously (expandable to 4 with a late-game studio expansion). Minimum 2 quarters between greenlight events (you cannot greenlight two films in the same quarter). This prevents decision flooding and forces the player to live with choices.

### 3.2 The Production Pipeline

Every film moves through six phases displayed on a physical wall-mounted board. Each phase has a duration (in quarters), a resource demand, and 3-5 key decision points.

#### Phase 1: DEVELOPMENT (2-3 quarters)

Resource demand: 1 Story Room slot, 1 Director.

Key decisions:
- **Story Structure**: Choose from 3 procedurally generated story outlines proposed by the assigned Story Artist. Each biases different Film DNA attributes. Outline A might favor HEART over HUMOR. Outline B favors SPECTACLE over STORY DEPTH.
- **Tone Calibration**: Set the target tone on two sliding axes -- Light/Dark and Grounded/Fantastical. This constrains which Voice Actors are appropriate and affects audience breadth.
- **Hidden Risk Reveal #1**: The first hidden risk (if any) is revealed. The player can address it now (costs +1 quarter in Development, +$5M) or gamble that it won't manifest later.

Phase output: STORY DEPTH base score (3-8 range depending on Story Artist skill, Director vision alignment, and time invested). This score can be modified later but the base is set here. A rushed Development (2 quarters) caps STORY DEPTH base at 6. Full Development (3 quarters) allows up to 8.

#### Phase 2: PRE-PRODUCTION (2-3 quarters)

Resource demand: 1 Story Room slot, Director, Lead Animator assignment, Voice Casting sessions.

Key decisions:
- **Storyboard Review**: The Director presents an animatic (represented as a series of storyboard panels on the corkboard with quality indicators). The player can approve, request revisions (+1 quarter, +$3M, STORY DEPTH +0.5), or override the director's approach (Director morale -15, risk of HEART score penalty, but redirects toward market preferences).
- **Voice Casting**: Select Voice Actors from available pool for 2-4 key roles. Each Voice Actor has a STAR POWER rating (1-10), a SALARY DEMAND ($500K to $15M per role), a SCHEDULING AVAILABILITY window, and a hidden CHEMISTRY modifier that interacts with other cast members. Casting a high-STAR POWER actor boosts VOICE CAST APPEAL but consumes budget. Chemistry bonuses are revealed post-recording.
- **Technical Pre-Vis**: If using CG, run a technical feasibility assessment. The film's TECHNICAL AMBITION is compared against your current tech tree. If ambition exceeds capability, choose: scale down ambition (SPECTACLE cap reduced), invest in rush R&D (cost x1.5, risk of tech failure), or proceed and accept render time overruns (PRODUCTION phase +1 quarter).
- **Hidden Risk Reveal #2**: Second risk tag (if present) revealed.

Phase output: VOICE CAST APPEAL score locked. Storyboard quality modifier applied to STORY DEPTH. Technical feasibility confirmed or flagged.

#### Phase 3: PRODUCTION (3-5 quarters)

Resource demand: Full animator team (4-12 animators depending on budget), Render Farm allocation (20-80% of capacity), Director.

This is the longest and most resource-intensive phase. The player's verb shifts from DECIDE to MANAGE.

Key decisions:
- **Animator Allocation**: Assign animators to the production. Each animator has a SPEED rating (1-10) and QUALITY rating (1-10) -- these are inversely weighted. A 9-SPEED / 4-QUALITY animator churns out footage fast but drags down ANIMATION QUALITY. A 3-SPEED / 9-QUALITY animator produces stunning work but slows the pipeline. The player must balance the team composition. Total team QUALITY average sets the ANIMATION QUALITY ceiling. Total team SPEED average determines quarters required.
- **Dailies Review**: Each quarter during Production, the player reviews "dailies" -- a snapshot of current animation quality. If ANIMATION QUALITY is trending below target, the player can: push the team harder (Crunch -- SPEED +2, animator morale -20 per quarter of crunch, quality variance increases), add more animators (cost increase, 1-quarter ramp-up delay), or accept the current trajectory.
- **Director Interference vs. Trust**: Each quarter, the Director may request a creative deviation -- adding a sequence, changing a character design, reworking a scene. Approving costs time/money but can boost HEART, ORIGINALITY, or STORY DEPTH. Denying preserves schedule but costs Director morale and may cap HEART. This is the Innovation vs. Formula axis made concrete at the production level.
- **Render Farm Crises**: If Render Farm allocation is above 60%, random crisis events can trigger -- hardware failures (lose 1 quarter of render progress), power costs spike ($2M unplanned expense), or a rival's film requires you to share render capacity if you've signed a co-processing agreement.

Phase output: ANIMATION QUALITY score locked. SPECTACLE base score set (driven by tech tree capabilities + animator quality + render investment). Production cost finalized.

#### Phase 4: POST-PRODUCTION (1-2 quarters)

Resource demand: Post-production team (auto-assigned from studio staff), Render Farm allocation (10-30%), Sound Design budget ($2M-$8M).

Key decisions:
- **Lighting and Effects Pass**: Invest additional budget ($3M-$10M) for enhanced lighting/effects. Each $3M invested adds +0.3 to SPECTACLE up to a cap of +1.5. Diminishing returns prevent brute-force spending.
- **Score and Sound**: Allocate sound budget. $2M = functional score (no DNA impact). $5M = quality score (HEART +0.3, REWATCHABILITY +0.2). $8M = signature score (HEART +0.5, REWATCHABILITY +0.5, chance of "Iconic Soundtrack" bonus that adds +10% to long-tail box office).
- **Test Screening**: Run a focus test. Costs $1M and 1 quarter. Returns a PROJECTED AUDIENCE SCORE (noisy estimate of final audience reception, accurate to +/- 15%). Based on results, the player can make one final adjustment: re-cut for pacing (HUMOR +0.5, STORY DEPTH -0.3), add a crowd-pleasing ending (AUDIENCE BREADTH +1, ORIGINALITY -0.5), or leave it as-is.
- **Final Director Showdown**: If the Director's morale is below 40, they demand a final creative concession -- typically restoring a cut sequence or removing a studio-mandated change. This is the last chance to either honor the artistic vision or assert commercial control. Consequences are significant: honoring the vision adds ORIGINALITY +0.5 and HEART +0.3 but may reduce AUDIENCE BREADTH. Overriding tanks Director morale to 0 (they will leave the studio after release) but preserves commercial positioning.

Phase output: Final SPECTACLE adjustments. REWATCHABILITY score set. All Film DNA scores finalized for review before marketing.

#### Phase 5: MARKETING (1-2 quarters)

Resource demand: Marketing budget ($5M-$40M), no studio production resources.

Key decisions:
- **Marketing Budget**: Determines AWARENESS score (0-100). Formula: `AWARENESS = 30 + (Marketing Budget / Max Budget) * 50 + Franchise Bonus + Star Power Bonus`. Awareness directly multiplies opening weekend revenue.
- **Trailer Strategy**: Choose which Film DNA attributes to emphasize in marketing. Emphasizing SPECTACLE attracts a wide audience but sets expectations that hurt if the film underdelivers. Emphasizing HEART attracts a loyal but smaller audience with better word-of-mouth multipliers. Emphasizing VOICE CAST APPEAL front-loads the box office (higher opening, steeper drop). The player can emphasize up to 2 attributes.
- **Release Date Finalization**: Lock the release quarter. Check rival release calendar. Releasing in the same quarter as a rival tentpole splits the audience pool. Releasing in a barren quarter gives 1.3x box office multiplier but may miss awards season eligibility (films must release Q3-Q4 for Oscar consideration).
- **Festival Circuit** (if Prestige reputation > 60): Submit to 1-2 festivals for early buzz. Costs $2M per festival. Success (Film DNA composite > 7.0) adds AWARENESS +10 and PRESTIGE +5. Failure (composite < 5.5) subtracts AWARENESS -5 and generates negative pre-release press.

Phase output: AWARENESS score. Release timing locked. Marketing narrative established (affects word-of-mouth trajectory shape).

#### Phase 6: RELEASE (4 weeks, auto-resolved with weekly decision points)

This phase plays out as the Box Office Gauntlet (see Section 3.5). The player watches but can make minor interventions:
- **Week 1**: Opening weekend results. If below projections, option to increase marketing spend (+$5M for +8 AWARENESS mid-run, diminishing effect).
- **Week 2**: Drop-off rate established. Word-of-mouth kicks in. High HEART + high AUDIENCE SCORE = low drop-off (legs). High SPECTACLE + low STORY DEPTH = high drop-off (frontloaded).
- **Week 3**: Competition effects. If a rival releases this week, your box office drops by 20-40% depending on genre overlap.
- **Week 4**: Final tally. Total domestic box office calculated. International multiplier applied (1.5x to 2.5x domestic based on SPECTACLE and VOICE CAST APPEAL). Home video / ancillary revenue calculated as 30-60% of theatrical gross.

Phase output: Total revenue. Profit/loss calculated. Reputation shifts applied. Awards eligibility determined.

### 3.3 The Talent Engine

Four talent categories, each with distinct mechanical roles.

#### Directors

- **Attributes**: VISION (1-10, determines ORIGINALITY and HEART ceiling for their films), EGO (1-10, determines how often they demand creative control and how badly they react to overrides), COMMERCIAL SENSE (1-10, determines how well they calibrate for audience), SPECIALTY (genre/tone tags -- "Epic," "Comedy," "Dark," "Intimate"), TRACK RECORD (list of past films and their scores).
- **Hiring**: Directors are available on the market each year. Top directors (VISION 8+) demand $2M-$5M per-film fees plus a profit participation deal (5-15% of net). Mid-tier directors cost $500K-$1.5M flat. Directors with a recent hit have inflated demands. Directors with a recent flop are cheaper but carry studio morale risk.
- **Retention**: After each film, a Director's loyalty is checked. Loyalty is influenced by: whether you supported their vision during production, whether the film was well-received, and whether rivals are offering better deals. A Director who leaves takes their TRACK RECORD to a rival -- and might make their masterpiece for someone else.
- **Director-Film Match**: When a Director's SPECIALTY tags match a film concept's genre/tone, they receive a +1 bonus to VISION for that production. Mismatched directors receive -1. A "Comedy" specialist directing an "Epic Dark" film is a recipe for a muddled tone -- unless their VISION is high enough to transcend genre.

#### Animators

- **Attributes**: SPEED (1-10), QUALITY (1-10), STYLE (2D Traditional, CG Generalist, CG Specialist -- Fur/Hair, Lighting, Character, Effects), MORALE (0-100), SALARY ($80K-$300K/year).
- **Team Dynamics**: Assigning 2+ animators of the same STYLE to a production triggers a SYNERGY bonus (+0.5 ANIMATION QUALITY). Assigning animators with conflicting style philosophies (a 2D purist and a CG-only specialist) triggers a FRICTION penalty (-0.3 ANIMATION QUALITY, morale drain for both).
- **Poaching**: Rival studios poach your animators based on their salary relative to market rate and morale. A morale-depleted animator with below-market salary has a 30% chance per year of being poached. The player is notified of poaching attempts and can counter-offer (salary increase) or let them go.
- **Crunch Mechanics**: Pushing animators into crunch (activated per-quarter during Production) boosts SPEED by +2 but costs 20 MORALE per quarter. At MORALE below 30, animators have a 15% chance per quarter of quitting with no warning. Crunch for 3+ consecutive quarters triggers a "Studio Culture" event that reduces all studio morale by 10 and makes future hiring 20% more expensive for 1 year. The game does not reward crunch as a free resource -- it is a loan against your studio's future.

#### Story Artists

- **Attributes**: NARRATIVE SKILL (1-10, determines quality of story outlines generated in Development), GENRE AFFINITY (tags matching film genres), COLLABORATION (1-10, determines how well they work with Directors -- high COLLABORATION + high Director EGO = smoother Development).
- **Function**: Story Artists generate the story outline options in Development Phase. Higher NARRATIVE SKILL = higher STORY DEPTH base potential. They also contribute to HEART during pre-production if assigned to storyboard duty.
- **Scarcity**: There are fewer elite Story Artists than elite animators. A NARRATIVE SKILL 9 Story Artist is a studio-defining asset. Losing one hurts immediately -- your next film's Development phase will feel the gap.

#### Voice Actors

- **Attributes**: STAR POWER (1-10), SALARY DEMAND ($500K-$15M per role), AVAILABILITY (quarters available for recording), ACTING QUALITY (1-10, separate from star power -- a 9-STAR 4-ACTING celebrity is a marketing asset but not a performance asset), CHEMISTRY MODIFIER (hidden, revealed post-recording, ranges from -0.5 to +1.0 and modifies VOICE CAST APPEAL based on specific cast pairings).
- **Market Dynamics**: Voice Actor salaries inflate 5-10% per year across the campaign (reflecting the historical trend of celebrity voice casting driving costs up). A Voice Actor whose last film was a hit demands 20% more. One whose last film bombed is 15% cheaper but carries an audience skepticism penalty (-0.3 VOICE CAST APPEAL for 1 year).
- **The Celebrity Trap**: High STAR POWER actors boost VOICE CAST APPEAL and opening weekend multiplier but at enormous cost. The optimal strategy is not "always hire the biggest star" -- it's matching ACTING QUALITY to the film's needs and STAR POWER to the marketing strategy. A $12M celebrity in a $60M film eats 20% of the budget for a stat that has diminishing returns above 7.

### 3.4 The Technology Tree (The Render Race)

A branching tech tree representing CG rendering and animation technology from 1995 to 2010. The tree has two main branches -- **CG Advancement** and **2D Innovation** -- with a **Hybrid** branch connecting them.

#### CG Branch (12 nodes)

Each node costs R&D budget ($3M-$15M) and takes 2-6 quarters to research.

| Node | Cost | Time | Effect |
|------|------|------|--------|
| Basic CG Modeling | $3M | 2Q | Unlocks CG production. ANIMATION QUALITY floor = 3 for CG films. |
| Texture Mapping v2 | $4M | 2Q | ANIMATION QUALITY floor +1 for CG films. |
| Basic Fur/Hair | $6M | 3Q | Unlocks "Fur/Hair" visual tag. SPECTACLE +0.5 for films using it. |
| Subsurface Scattering | $8M | 4Q | Realistic skin rendering. ANIMATION QUALITY ceiling +1 for character-driven CG films. |
| Advanced Fur/Hair | $10M | 4Q | Requires Basic Fur/Hair. SPECTACLE +1.0 for films using it. Enables realistic animal characters. |
| Fluid Dynamics | $8M | 3Q | Unlocks water/liquid effects. SPECTACLE +1.0 for films featuring water environments. |
| Facial Rigging v2 | $7M | 3Q | HEART ceiling +0.5 for CG films (better emotional expression). |
| Crowd Systems | $6M | 3Q | Enables large-scale crowd scenes. SPECTACLE +0.5. Reduces animator count needed for epic films by 2. |
| Global Illumination | $12M | 5Q | Photorealistic lighting. ANIMATION QUALITY ceiling +2 for CG films. Game-changer node. |
| Advanced Facial Rigging | $10M | 4Q | Requires Facial Rigging v2. HEART ceiling +1.0 for CG films. Enables "subtle performance" -- characters can convey complex emotion. |
| Real-Time Preview | $8M | 3Q | Reduces Production phase by 1 quarter for CG films. Director can iterate faster = ORIGINALITY +0.3. |
| Physically Based Rendering | $15M | 6Q | Requires Global Illumination. ANIMATION QUALITY ceiling +2. SPECTACLE +1.0. The definitive late-game CG node. |

#### 2D Innovation Branch (6 nodes)

| Node | Cost | Time | Effect |
|------|------|------|--------|
| Digital Ink & Paint | $3M | 2Q | Reduces 2D Production phase by 1 quarter. Cost reduction of $5M for 2D films. |
| Multiplane Digital Camera | $5M | 3Q | SPECTACLE +1.0 for 2D films. Depth and parallax effects. |
| Stylized Rendering | $6M | 3Q | Unlocks unique visual style options. ORIGINALITY +1.0 for 2D films. |
| Digital 2D Effects | $7M | 4Q | SPECTACLE +1.0 for 2D films. Fire, water, magic effects without CG. |
| Hand-Drawn/CG Compositing | $8M | 4Q | Unlocks Hybrid technology approach. ANIMATION QUALITY +1 for Hybrid films. |
| 2D Master Suite | $10M | 5Q | Requires all previous 2D nodes. ANIMATION QUALITY ceiling = 10 for 2D films. ARTISTIC COURAGE +10 reputation when releasing a 2D film post-2003. |

#### Hybrid Branch (3 nodes, requires Hand-Drawn/CG Compositing)

| Node | Cost | Time | Effect |
|------|------|------|--------|
| Seamless Integration | $8M | 4Q | ANIMATION QUALITY +1 for Hybrid films. Eliminates visual "seam" penalty. |
| Style Transfer Pipeline | $10M | 5Q | Allows CG films to adopt 2D visual aesthetics. ORIGINALITY +1.5. |
| Unified Render Engine | $12M | 5Q | Full tech ceiling for both 2D and CG in a single pipeline. ANIMATION QUALITY ceiling = 10 for any approach. |

**The strategic tension**: CG is the future -- the market rewards it, audiences expect it after 2000, and CG tech improvements have compounding effects. But 2D innovation is cheaper, builds ARTISTIC COURAGE reputation, and creates high-ORIGINALITY films that can win awards and attract prestige talent. The Hybrid path is expensive but versatile. There is no "correct" tech strategy -- only strategies that align or clash with your overall studio identity.

**Mid-production application rule**: If a tech breakthrough completes while a film is in Production or earlier, the player can apply it to that film at a cost of +$3M and +1 quarter delay (retrofitting). This creates a meaningful timing decision: do you rush a tech node to hit a current production, or let it benefit the next film cleanly?

### 3.5 The Box Office Gauntlet

When a film enters Release, the Box Office Gauntlet takes over. This is a 4-week auto-resolving sequence with weekly player check-ins and dramatic presentation.

**Opening Weekend Formula**:

```
Opening Weekend ($M) = Base * Awareness Multiplier * Star Power Modifier
                       * Season Modifier * Competition Modifier

Where:
  Base = (Budget / 4) * (Film DNA Composite / 7)
  Film DNA Composite = weighted average of all 8 DNA scores
    Weights: STORY 1.0, ANIMATION 1.0, HUMOR 0.8, HEART 0.8,
             SPECTACLE 1.2, VOICE CAST 0.6, ORIGINALITY 0.5, REWATCHABILITY 0.3
  Awareness Multiplier = 0.5 + (AWARENESS / 100)
  Star Power Modifier = 1.0 + (Highest Voice Actor STAR POWER * 0.03)
  Season Modifier = Summer (1.3), Holiday (1.4), Spring (0.9), Fall (1.0)
  Competition Modifier = 1.0 if no rival release, 0.6-0.8 if competing
```

**Weekly Drop-off Formula**:

```
Week N Revenue = Opening Weekend * Drop Rate ^ (N-1) * WOM Modifier

Where:
  Base Drop Rate = 0.45 (default 55% drop per week)
  Drop Rate adjusted by:
    +0.05 (less drop) per point of HEART above 6
    +0.03 per point of REWATCHABILITY above 6
    -0.05 (more drop) per point of SPECTACLE above STORY DEPTH
    -0.03 if marketing emphasized SPECTACLE but film underdelivered
  WOM Modifier = starts at 1.0, increases by 0.02 per point of
    (HEART + STORY DEPTH) above 12 combined, can reach 1.15 max
```

**Critic Reviews (The Projector Score)**:

```
Projector Score (0-100) = (Film DNA Composite * 10) + Originality Bonus
                          + Director Prestige Bonus + Era Alignment Bonus
                          + Random Variance (-5 to +5)

Where:
  Originality Bonus = ORIGINALITY * 2 (critics reward novelty)
  Director Prestige Bonus = Director's TRACK RECORD average * 1.5
  Era Alignment Bonus = +5 if film matches current critical trends
    (e.g., CG films score +5 in 2000-2005, 2D films score +5 in 1995-1998,
     Hybrid/Stylized score +5 in 2006-2010)
```

**Audience Score (separate from Projector Score)**:

```
Audience Score (0-100) = HUMOR * 3 + HEART * 3 + SPECTACLE * 2
                         + VOICE CAST APPEAL * 1.5 + REWATCHABILITY * 2
                         - (STORY DEPTH - 5).abs * 1.0
                         (audiences penalize both too-simple and too-complex stories)
```

**Awards Season**: Films releasing Q3-Q4 are eligible for the Best Animated Feature award (established in-game in 2001). Award nomination probability is based on Projector Score ranking among all films released that year (yours and rivals'). Top 5 Projector Scores are nominated. Winner is determined by a weighted vote:

```
Award Score = Projector Score * 0.4 + STORY DEPTH * 8 + HEART * 6
              + ORIGINALITY * 6 + ANIMATION QUALITY * 5 + Studio PRESTIGE * 0.1
```

Winning Best Animated Feature: PRESTIGE +15, all talent loyalty +10, next film's marketing efficiency +20%, significant cultural moment for the studio.

### 3.6 Film DNA System

Every film is defined by 8 DNA attributes, each scored 0.0-10.0:

| Attribute | Determined By | Impact |
|-----------|--------------|--------|
| STORY DEPTH | Story Artist skill, Development phase time, Director VISION, story outline choice | Critic score, award chances, long-term reputation |
| ANIMATION QUALITY | Animator team QUALITY average, tech tree state, render farm investment, Production phase time | Critic score, visual spectacle floor, studio technical reputation |
| HUMOR | Director specialty, Story Artist genre affinity, tone calibration, focus test adjustments | Audience score, opening weekend, rewatchability |
| HEART | Director VISION, Development/Pre-Production investment, Director morale at wrap, score/sound budget | Critic score, word-of-mouth multiplier, award chances, long-tail box office |
| SPECTACLE | Tech tree capabilities, budget, animator team + render farm investment, Post-Production effects budget | Opening weekend, international multiplier, marketing impact |
| VOICE CAST APPEAL | Voice Actor STAR POWER + ACTING QUALITY + CHEMISTRY, number of recognizable names | Opening weekend, marketing efficiency, audience score |
| ORIGINALITY | Concept ORIGINALITY score, Director VISION, player's creative decisions (supporting vs. overriding director), studio Innovation reputation | Critic score (high variance), award chances, long-tail performance |
| REWATCHABILITY | HUMOR + HEART combined, score/sound investment, overall DNA balance (films with no weak scores have higher rewatchability) | Home video revenue, cultural longevity, franchise potential |

**Interaction effects** (these are the deep system hooks that create emergent strategy):

- HEART multiplies STORY DEPTH for critic scores: `Effective Story = STORY DEPTH * (1 + HEART * 0.05)`. A film with 8 STORY and 8 HEART has effective story of 11.2 for critics. This rewards emotional storytelling over technically complex plotting.
- VOICE CAST APPEAL has diminishing returns above 7: each point above 7 adds only 50% of normal impact to box office. Spending $30M on voice talent to push from 8 to 9 is almost never worth it.
- ORIGINALITY is the highest-variance stat: films with ORIGINALITY 8+ have a +/- 3 random modifier on their Projector Score (critics either love or hate bold swings). Films with ORIGINALITY 3 or below have +/- 0.5 (safe films get safe reviews). This makes artistic courage a genuine gamble -- not a reliable path.
- SPECTACLE without STORY DEPTH creates frontloaded films: high opening weekend, steep drop-off, low award chances, low cultural longevity. The "DreamWorks model" -- profitable but soul-emptying.
- High REWATCHABILITY extends a film's revenue tail and builds franchise goodwill. A franchise built on rewatchable films can sustain 3-4 sequels before fatigue. A franchise built on SPECTACLE burns out after 2.

### 3.7 Studio Soul and the Innovation vs. Formula Axis

Every studio has an invisible SOUL score ranging from -100 (Pure Executive) to +100 (Pure Artist). Starting value: 0 (neutral).

**Actions that shift toward Artist (+)**:
- Greenlighting a concept with ORIGINALITY 7+ : +5
- Supporting a Director's creative deviation during Production: +3
- Releasing a 2D film after 2003: +8
- Accepting a test screening score below 50 and releasing anyway: +5
- Investing in 2D Innovation tech tree nodes: +3 per node
- Refusing to greenlight a sequel: +4

**Actions that shift toward Executive (-)**:
- Greenlighting a sequel: -3
- Overriding a Director's creative vision: -3
- Cutting a film's Development phase short: -2
- Choosing marketing emphasis on VOICE CAST APPEAL or SPECTACLE: -1
- Closing your 2D animation division: -10
- Focus-testing and then changing the ending: -4
- Greenlighting a concept specifically because it has high AUDIENCE BREADTH: -2

**The SOUL score is hidden from the player.** They see its effects but not the number:

- SOUL > 50: "Auteur Studio" -- attracts high-VISION Directors (+2 VISION for all Directors while at this level), prestige talent takes salary cuts to work here (-20% salary), but commercial Voice Actors charge more (+15% salary) and AUDIENCE BREADTH calculations receive a -0.5 penalty (you're seen as "arthouse").
- SOUL 20 to 50: "Creator-Led Studio" -- balanced benefits. +1 VISION for Directors, no salary modifiers. Slight ORIGINALITY bonus (+0.3) on all films.
- SOUL -20 to 20: "Balanced Studio" -- no modifiers. The safe middle.
- SOUL -50 to -20: "Commercial Powerhouse" -- AUDIENCE BREADTH +0.5, marketing efficiency +10%, but top-tier Directors avoid you (-2 VISION for recruiting purposes) and ORIGINALITY ceiling capped at 7.
- SOUL < -50: "Formula Factory" -- AUDIENCE BREADTH +1.0, sequel fatigue accumulates 30% slower, but ORIGINALITY ceiling capped at 5, all Directors with VISION 8+ refuse to work here, and each film has a 10% chance of a "Critical Backlash" event where Projector Score drops by 15 regardless of quality. You've become the thing critics love to hate.

The system never tells the player they're becoming a formula factory. It shows them through consequences -- the directors who won't return calls, the reviews that feel unfairly harsh, the Projector Scores that don't match the quality they thought they built. The player has to read the system through its outputs. That's where the emotional depth lives.

---

## 4. SYSTEMS INTERACTION MAP

This is where FRAMEWAR becomes more than a series of subsystems. Every mechanic feeds into every other. Here's the full map:

```
GREENLIGHT TABLE
  |---> PRODUCTION PIPELINE (commits resources for 3-4 years)
  |---> TALENT ENGINE (Director assigned, anchors the production)
  |---> TECH TREE (technology approach chosen, determines tech requirements)
  |---> ECONOMY (budget committed, reduces available funds)
  |---> STUDIO SOUL (concept choice shifts identity axis)

PRODUCTION PIPELINE
  |---> FILM DNA (every phase decision modifies DNA scores)
  |---> TALENT ENGINE (animators assigned, Director morale tracked)
  |---> TECH TREE (tech capabilities constrain/enable DNA ceilings)
  |---> ECONOMY (phase costs accumulate, overruns possible)
  |---> STUDIO SOUL (creative decisions during production shift axis)

TALENT ENGINE
  |---> PRODUCTION PIPELINE (talent quality determines DNA ceilings)
  |---> FILM DNA (Director VISION, Animator QUALITY, Story Artist SKILL feed scores)
  |---> ECONOMY (salaries, hiring costs, retention costs)
  |---> GREENLIGHT TABLE (available Directors determine viable concepts)
  |---> STUDIO SOUL (talent retention affected by soul position)

TECH TREE
  |---> PRODUCTION PIPELINE (tech capabilities set quality floors/ceilings)
  |---> FILM DNA (tech nodes directly modify ANIMATION QUALITY, SPECTACLE)
  |---> ECONOMY (R&D costs)
  |---> GREENLIGHT TABLE (tech state determines viable technology approaches)
  |---> BOX OFFICE (audience expectations for CG quality rise over time)

BOX OFFICE GAUNTLET
  |---> ECONOMY (revenue from theatrical, home video, ancillary)
  |---> REPUTATION (Projector Score, Audience Score, Awards shift 4 axes)
  |---> TALENT ENGINE (film success/failure affects loyalty, salary demands)
  |---> GREENLIGHT TABLE (revenue determines next film's budget capacity)
  |---> STUDIO SOUL (how you market and release shifts the axis)

FILM DNA
  |---> BOX OFFICE (all DNA scores feed revenue formulas)
  |---> REPUTATION (DNA scores determine critical/audience/awards reception)
  |---> STUDIO SOUL (the DNA profile of your filmography IS your identity)

REPUTATION (4 axes: Prestige, Commercial, Technical, Artistic Courage)
  |---> TALENT ENGINE (reputation determines who wants to work with you)
  |---> GREENLIGHT TABLE (reputation determines what pitches arrive)
  |---> BOX OFFICE (Prestige affects award chances; Commercial affects audience trust)
  |---> ECONOMY (reputation affects marketing efficiency and distribution deals)

ECONOMY
  |---> GREENLIGHT TABLE (budget pool limits what you can greenlight)
  |---> TECH TREE (R&D budget allocation)
  |---> TALENT ENGINE (salary capacity)
  |---> PRODUCTION PIPELINE (budget constrains phase investment)
```

**Key Feedback Loops**:

1. **Positive loop (Prestige Spiral)**: Make a critically acclaimed film -> win awards -> PRESTIGE rises -> attract better Directors -> better Directors make better films -> more awards. This loop is powerful but fragile -- one over-budgeted flop can break the cycle by draining the economy.

2. **Positive loop (Commercial Flywheel)**: Make a profitable film -> more budget available -> bigger marketing budgets -> higher awareness -> bigger opening weekends -> more profit. This loop is stable but has diminishing creative returns -- audience fatigue and formula penalties erode quality over time.

3. **Negative loop (Innovation Tax)**: Push artistic boundaries -> ORIGINALITY high variance causes unpredictable reviews -> box office volatility -> budget instability -> pressure to play safe on the next film. This is the brake that prevents "always be innovative" from being a dominant strategy.

4. **Negative loop (Sequel Fatigue)**: Sequels generate safe revenue -> sequel revenue funds more sequels -> franchise fatigue accumulates -> each sequel earns less -> eventually the franchise collapses. This prevents "always make sequels" from being dominant.

5. **Tension loop (Art vs. Commerce)**: Artistic films build PRESTIGE and ARTISTIC COURAGE but cost more relative to revenue. Commercial films build budget capacity but erode STUDIO SOUL. The player must oscillate between these poles -- one commercial tentpole funding one artistic risk is the balanced strategy, but the game tempts you to lean hard in either direction.

---

## 5. PROGRESSION DESIGN

### 5.1 Campaign Arc (1995-2010)

The campaign spans 60 in-game quarters (15 years, 4 quarters/year). At default game speed, the full campaign takes 8-12 hours.

#### Era 1: The Dawn (1995-1998) -- Quarters 1-16

- **Studio state**: Small. 1 active production slot, 15-20 staff, $60M starting budget, basic CG and 2D capability.
- **Era events**: CG revolution begins. The first CG-animated blockbuster has just shocked the industry (not named, but the player understands the reference). 2D studios are still dominant but nervous. Voice actor costs are reasonable ($1M-$3M for top talent).
- **Player experience**: Learning the pipeline. Your first film is modest -- $40M-$60M budget, limited tech, a small team. The emphasis is on understanding how Development decisions cascade into Production outcomes and how Film DNA emerges from your choices. The first box office experience is a tutorial in reading the revenue formula.
- **Progression milestones**: Complete first film. Achieve first profitable release. Hire first elite Director (VISION 7+). Unlock 3+ tech tree nodes.
- **Difficulty**: Low. Rival studios are establishing themselves. Competition for box office and awards is moderate. Mistakes are survivable.

#### Era 2: The Arms Race (1999-2002) -- Quarters 17-32

- **Studio state**: Growing. 2 active production slots unlocked (requires $20M studio expansion investment). 30-40 staff. Budget pool depends on Era 1 performance ($80M-$200M).
- **Era events**: CG technology accelerates. Multiple rival studios enter the market. Voice actor salaries begin inflating. The Best Animated Feature Oscar is established (2001, Quarter 25) -- suddenly there's a prestige meta-game. Audience expectations for CG quality rise sharply. 2D films begin underperforming at the box office.
- **Player experience**: Juggling two simultaneous productions for the first time. Learning resource allocation across competing films. The Oscar creates a new strategic dimension -- timing releases for awards eligibility, investing in STORY DEPTH and HEART for award contention. The first major rival release that directly competes with your film.
- **Progression milestones**: Manage two simultaneous productions. Achieve first $200M+ gross. Receive first Oscar nomination. Navigate first production crisis (budget overrun, director conflict, or talent departure).
- **Difficulty**: Medium. Competition intensifies. The 2D vs. CG decision becomes urgent. Budget management matters -- one flop can set you back a year.

#### Era 3: The Shakeout (2003-2005) -- Quarters 33-44

- **Studio state**: Mature or struggling, depending on Era 2 performance. 2-3 active production slots. 40-60 staff. The 2D question is existential.
- **Era events**: 2D animation collapses commercially. Multiple studios close their 2D divisions (or shut down entirely). Voice actor salaries peak. A rival studio releases a massive franchise-launching hit. The "comedy with celebrity voices" formula becomes the default -- and audiences are getting tired of it. CG technology reaches a quality plateau (baseline expectations are high).
- **Player experience**: Crisis management. If you invested heavily in 2D, you face a reckoning: close the division (lose 2D staff, save costs, ARTISTIC COURAGE drops) or keep it alive (bleed money, build ARTISTIC COURAGE, hope for a cultural shift that may never come). If you invested in CG, you're competing in a crowded market where technical quality alone no longer differentiates. The innovation pressure is intense.
- **Progression milestones**: Survive without going bankrupt. Make the 2D decision. Win or lose your first Oscar. Release your first sequel (or consciously refuse to). Navigate your first staff layoff.
- **Difficulty**: High. This is the campaign's crucible. Financial pressure peaks. Wrong bets are punished severely. The player who coasted on a single strategy is forced to adapt.

#### Era 4: The Maturation (2006-2008) -- Quarters 45-56

- **Studio state**: Established identity. The player's STUDIO SOUL has crystallized through dozens of decisions. 2-3 active slots. Premium talent either seeks you out or avoids you based on reputation.
- **Era events**: The animation market stabilizes. Quality expectations are very high -- a mediocre CG film no longer succeeds on novelty. Franchise fatigue is a real market force. An indie animation movement begins (small studios making stylized, lower-budget films that win critical acclaim). International markets become a major revenue factor.
- **Player experience**: The player's strategy is mature. They understand the systems deeply enough to make sophisticated plays: timing tech breakthroughs to coincide with productions, casting Voice Actors for chemistry rather than star power, reading the rival release calendar and counter-programming. The emotional register shifts from "survival" to "legacy building."
- **Progression milestones**: Build a franchise (or choose not to). Release a film that defines your studio's identity. Hire a "legend" Director (VISION 10). Reach the top tier in at least one reputation axis.
- **Difficulty**: Medium-high. The systems are deep but the player has mastered them. The challenge is optimization and legacy curation rather than survival.

#### Era 5: Legacy (2009-2010) -- Quarters 57-60

- **Studio state**: Full maturity. The player's filmography is 6-10 films. The final 1-2 productions are in pipeline.
- **Era events**: A new era is dawning -- streaming, international co-productions, the rise of CG animation in new markets. The game signals that the era is ending.
- **Player experience**: The final film. The player greenlights their last production knowing it's the capstone. Every decision carries the weight of "this is what I want to be remembered for." The campaign ends with a retrospective: a procedurally generated "studio legacy" summary showing your complete filmography, total revenue, awards won, reputation profile, and procedurally generated critical commentary on your studio's place in animation history.
- **Difficulty**: Variable. The player can coast or go for broke.

### 5.2 Reputation System (4 Axes)

Reputation is tracked across 4 axes, each 0-100:

- **PRESTIGE** (gold): Built by critical acclaim, award wins, and high Projector Scores. Decays if you release consecutive films with Projector Score below 60.
- **COMMERCIAL APPEAL** (green): Built by box office success and profitable releases. Decays if you release consecutive flops.
- **TECHNICAL INNOVATION** (blue): Built by pushing tech tree, releasing films that showcase new capabilities, and achieving high ANIMATION QUALITY scores. Decays as tech becomes industry standard (a breakthrough from 2001 doesn't impress in 2006).
- **ARTISTIC COURAGE** (purple): Built by high-ORIGINALITY releases, championing 2D, supporting Director vision over commercial pressure, and making films that defy market expectations. Decays if you release formulaic content (low ORIGINALITY, sequels).

Each axis affects the game world:
- PRESTIGE > 70: Eligible for "Prestige Slate" pitches (high-ORIGINALITY, award-caliber concepts that only arrive at elite studios).
- COMMERCIAL > 70: Distribution deals improve (marketing efficiency +15%, international multiplier +0.2).
- TECHNICAL > 70: Tech tree research time reduced by 20%. Rival studios attempt to poach your animators more aggressively.
- ARTISTIC COURAGE > 70: Indie filmmakers seek you out (access to unique low-budget, high-ORIGINALITY pitches). Critical review baseline increases (+3 Projector Score for all films).

---

## 6. ECONOMY DESIGN

### 6.1 Budget Pool

The player manages a single studio budget pool in millions of dollars. Starting budget: $60M.

Income sources:
- **Theatrical Box Office** (net studio share = 45% of domestic gross, 35% of international gross)
- **Home Video/Ancillary** (30-60% of theatrical gross, paid out 2 quarters after theatrical release)
- **Merchandise Licensing** (available for films with REWATCHABILITY 7+, generates $5M-$30M over 4 quarters post-release, scaled to AUDIENCE BREADTH)
- **Sequel Greenlight Advance** (if a film has SEQUEL POTENTIAL 7+ and earned $150M+ theatrical, distributors offer a $20M advance on a sequel greenlight)

Expenses:
- **Film Production Budgets** ($40M-$180M per film, paid across production phases)
- **Staff Salaries** ($80K-$300K/year per animator, $200K-$500K/year per Story Artist, Director per-film fees separate)
- **Voice Actor Fees** ($500K-$15M per role, per film)
- **Technology R&D** ($3M-$15M per tech node)
- **Marketing** ($5M-$40M per film)
- **Studio Expansion** ($20M per production slot upgrade, $10M per Render Farm upgrade)
- **Overhead** (fixed $2M/quarter -- covers studio maintenance, non-creative staff)

### 6.2 Economic Tension Points

- **The Three-Year Cash Gap**: A film costs money for 3-4 years before generating any revenue. The player must manage cash flow across this gap. Greenlighting aggressively can create a cash crunch even if all films are eventually profitable.
- **The Tentpole-Prestige Balance**: A $150M commercial tentpole might gross $500M (net $180M studio share) and fund two $60M prestige films that gross $120M each (net $43M each, combined $86M). The tentpole subsidizes the art. But if the tentpole flops, the prestige films have no safety net.
- **Salary Inflation**: Staff salaries increase 3-5% per year. Voice actor salaries increase 5-10% per year. Technology R&D costs increase as you move up the tree. The player must grow revenue faster than costs or face a squeeze.
- **Sequel Economics**: A sequel costs 70% of the original's budget (reusable assets, established pipeline) and opens at 120% of the original's opening weekend (built-in audience). But ORIGINALITY is capped at 5 for first sequel, 3 for second sequel, 2 for third sequel. Sequel fatigue reduces each sequel's total gross by 15% from the predecessor (before any quality modifiers). The economic incentive to make sequels is real and powerful -- and the creative cost is equally real.
- **The Bankruptcy Threshold**: If the budget pool drops below -$30M, the studio enters CRISIS MODE. Crisis Mode forces the player to: lay off 30% of staff (player chooses who), cancel one active production (player chooses which, sunk costs are lost), and accept a distribution deal that gives unfavorable revenue splits (-10% on next 2 releases) in exchange for a $40M emergency loan. Crisis Mode is survivable but devastating. It should happen to players who over-extended -- not to players who made one bad film.

### 6.3 Sample Economic Flow

A concrete example of a mid-game economic cycle:

- **Year 2003, Q1**: Budget pool = $120M. Active productions: "TIDEWALKER" (CG, $90M budget, in Production Q3/5) and "FOLDED" (Hybrid, $55M budget, in Development Q2/3).
- **Quarterly expenses**: $8M (TIDEWALKER production phase), $3M (FOLDED development phase), $3M (staff salaries), $2M (overhead), $4M (tech R&D -- researching Advanced Fur/Hair). Total: $20M.
- **Q1 end**: Budget = $100M.
- **Q2**: TIDEWALKER enters Post-Production. Expenses drop to $15M/quarter. Budget = $85M.
- **Q3**: TIDEWALKER released. Opening weekend $42M. 4-week domestic total: $138M. International: $195M. Studio share: $62M + $68M = $130M. Budget = $85M - $15M + $130M = $200M. Home video income ($55M) arrives Q1 next year.
- **Q4**: Greenlight new film "SIGNAL" ($70M budget). Hire celebrity voice cast ($8M total). Budget = $200M - $8M - overhead = $187M.

This is a healthy studio. A single flop (TIDEWALKER grosses $60M instead of $333M total) would leave the player at $85M - $15M + $20M = $90M -- survivable but tight, with no room for the next greenlight without cutting scope.

---

## 7. RISK ASSESSMENT

What could make FRAMEWAR unfun? I've shipped games with broken loops. Here's where this design is most vulnerable.

### Risk 1: Death by Spreadsheet

**The threat**: The Production Pipeline has six phases with 3-5 decisions each. Multiply by 2-3 simultaneous films. That's 36-90 decision points per film cycle. If each decision feels like adjusting a slider on a spreadsheet, the player will drown in micro-management and lose the creative fantasy.

**The mitigation**: Decisions must be presented as narrative moments, not data inputs. "Your director wants to add a dream sequence to Act 2" is the same mechanical decision as "+1 quarter, +$3M, HEART +0.5" -- but the first creates emotional engagement and the second creates tedium. Every decision point needs a narrative wrapper. Additionally, the game should auto-resolve low-stakes decisions (e.g., routine render allocation when there's no contention) and only surface choices that involve genuine tradeoffs.

**Playtest priority**: HIGHEST. Build 10 decision points with narrative wrappers. Have players manage them across 2 films for 30 minutes. If they feel like a studio head, we're good. If they feel like an accountant, we redesign the decision presentation layer before building anything else.

### Risk 2: Opacity of Film DNA

**The threat**: The player makes 30+ decisions that feed into 8 DNA scores that feed into review/revenue formulas. If the player cannot trace the causal chain from "I approved that storyboard revision" to "my film scored 7.2 in STORY DEPTH" to "critics gave it 78 on the Projector Score," the game feels random. And if it feels random, player agency is an illusion.

**The mitigation**: After every phase gate, show the player a Film DNA preview -- the current estimated scores with clear attribution. "STORY DEPTH: 6.8 (Story Artist base 5.5 + Director vision +0.8 + extended Development +0.5)." After release, the post-mortem screen shows every decision that contributed to each DNA score. The player must always be able to answer "why did my film succeed/fail?" within 30 seconds of looking at the results screen.

**Playtest priority**: HIGH. Build the post-mortem screen early. Test whether players can retroactively understand their outcomes.

### Risk 3: The Mid-Campaign Sag

**The threat**: Hours 4-7 of a 10-hour campaign. The player has mastered the basics. The pipeline is familiar. But the late-game systems (complex tech tree, franchise management, multi-film strategy) haven't fully materialized. The game risks feeling repetitive as the player manages pipeline cycle #4 and #5 with the same tools and no new challenges.

**The mitigation**: Era events are the pacing mechanism. The 2D collapse (Era 3) is designed to be a mid-campaign earthquake that forces strategic pivots. The Oscar introduction (Era 2) adds a new strategic dimension. Rival studio escalation ensures the competitive landscape never stabilizes. The game should introduce at least one new system or major event every 3-4 film cycles. Additionally: the Studio Soul consequences should become more visible and more impactful in the mid-campaign, so the player starts seeing the identity they've built manifest in tangible ways (talent refusing to work with you, unique pitch concepts arriving, review patterns shifting).

**Playtest priority**: HIGH. Run a full campaign playtest with pacing instrumentation -- log every point where the player pauses, speeds up time, or alt-tabs. Those are the boredom signals.

### Risk 4: Sequel Dominance

**The threat**: Sequels are cheaper and more predictable. A rational optimizer will greenlight sequels whenever possible and dominate the economy. If the "correct" strategy is always sequels, the Innovation vs. Formula axis is decorative rather than meaningful.

**The mitigation**: Sequel fatigue is a hard mechanical brake -- 15% gross reduction per sequel, ORIGINALITY cap that increasingly hurts Projector Scores. Additionally, the Studio Soul penalties for over-sequelizing (Director talent drain, critical backlash chance) create long-term costs that offset short-term gains. The key balance number: a franchise's third sequel should be *roughly break-even* in expected value, making the fourth a losing proposition. First sequels should be clearly profitable. Second sequels should be a judgment call. This creates a decision gradient rather than a binary.

**Playtest priority**: MEDIUM. Model the sequel economy in a spreadsheet. Run 100 simulated franchise arcs. Tune the fatigue curve until the third sequel is marginal.

### Risk 5: The 2D Trap

**The threat**: The game's narrative heart is the death of 2D animation. But if investing in 2D is mechanically suicidal (which it historically was, commercially), then the "artistic courage" path isn't a real choice -- it's a trap for players who didn't read the meta. The game would be punishing thematic engagement.

**The mitigation**: 2D must be mechanically viable as a niche strategy, even if it's not the dominant one. The 2D Innovation tech tree is deliberately cheaper than CG. 2D films have lower budgets (smaller financial risk). ARTISTIC COURAGE reputation above 70 provides critical review bonuses that partially offset commercial disadvantage. The 2D Master Suite endgame node makes late-era 2D films award-competitive. A 2D-focused studio should be able to survive and win awards -- it just can't compete on raw box office with CG tentpoles. That's historically accurate AND mechanically fair. The player who champions 2D is playing a different game -- a prestige game rather than a revenue game -- and both paths should lead to satisfying campaign conclusions.

**Playtest priority**: MEDIUM. Run two complete campaign playthroughs -- one all-CG, one 2D-focused. Both should be completable. The 2D playthrough should feel harder but more emotionally resonant.

### Risk 6: Information Overload in Late Game

**The threat**: By Era 4, the player is managing 3 simultaneous productions, a roster of 50+ staff, an advanced tech tree, franchise decisions, awards strategy, and rival studio positioning. The cognitive load may exceed what's fun.

**The mitigation**: The diegetic UI is the first defense -- information is spatial (walk to the render farm to see render status, walk to the storyboard room to see story progress) rather than stacked in menus. The second defense is an "advisor" system: procedurally generated suggestions from your lead Story Artist ("I think SIGNAL needs more development time -- the second act isn't landing"), your CFO ("We can't afford another $150M greenlight this year"), and your tech lead ("Our render farm is at 85% capacity -- we need an upgrade before the next production starts"). Advisors surface the most critical information without the player having to seek it. The third defense: the game speed slider. Players who want to process carefully can slow down. Players who are in flow can speed up.

**Playtest priority**: MEDIUM. Late-game UI/UX test with 5 players who've completed the campaign. Measure time-to-decision and self-reported cognitive load.

### Risk 7: Rival Studios Feel Like Wallpaper

**The threat**: If rival studios are just names that occasionally release competing films, the competitive dimension is shallow. The "war" in FRAMEWAR needs to feel like a rivalry, not a weather system.

**The mitigation**: Rival studios need readable strategies and persistent identities. Each rival has a visible studio profile (their reputation across 4 axes, their filmography, their tech level, their star talent). The player should be able to look at a rival and say "they're going for the Oscar this year with their prestige film -- I need to either compete or dodge." Rivals should poach talent from you (and you from them). Rivals should occasionally counter-program your releases. The player should develop a relationship with each rival -- grudging respect, fierce competition, strategic avoidance. 2-3 rival studios, each with a distinct personality, is the target. More than that and they blur together.

**Playtest priority**: MEDIUM. Build one rival studio AI with full behavior. Test whether players develop an emotional relationship with it over a campaign.

---

## 8. OPEN QUESTIONS FOR PLAYTESTING

These are the questions I cannot answer from the design chair. They require hands on the game.

1. **Decision density per quarter**: Is 3-5 decisions per phase per film the right number? It might be 2-3 with more weight per decision. The playtest will tell us whether the player feels engaged or overwhelmed.

2. **Game speed and real-time feel**: Should the game run in real-time with pause, or in discrete turn-based quarters? Real-time creates urgency and atmosphere. Turn-based creates clarity and reduces stress. The target audience (management sim players) trends toward turn-based, but the diegetic studio fantasy benefits from real-time presence. Hypothesis: real-time with liberal auto-pause on important events.

3. **Procedural film concept quality**: Can 100+ authored templates with variable elements feel hand-crafted on the 6th playthrough? The concept generator is the game's content engine. If concepts feel algorithmic, the greenlight decision loses its magic. This needs extensive testing with real film-literate players.

4. **Campaign length**: 8-12 hours is the target. Too short and the studio identity arc doesn't develop. Too long and the mid-campaign sag (Risk 3) becomes fatal. The right length will depend on pacing instrumentation from full campaign playtests.

5. **Difficulty tuning for the 2D path**: How much financial pressure is "hard but viable" vs. "unfun"? The 2D-focused studio needs to feel like an underdog, not a victim.

6. **Director personality system depth**: How complex do Director agents need to be? A Director with 3 attributes (VISION, EGO, COMMERCIAL SENSE) might be sufficient. A Director with 10 attributes might create richer stories but overwhelm the player's ability to evaluate hiring decisions. Start simple, add complexity if playtesting reveals a desire for deeper interpersonal dynamics.

7. **Box Office presentation pacing**: The 4-week Gauntlet needs to feel dramatic. Is a week-by-week reveal with animated numbers and competitor tracking compelling, or does it feel like waiting? Should the player be able to speed through it after the first few films? Does the drama hold up on the 8th release?

8. **Endgame retrospective format**: The campaign ends with a studio legacy summary. What form should this take? A static scorecard? A narrated retrospective? A procedurally generated "documentary" about your studio? The emotional landing of the campaign depends on this screen. It needs to make the player feel that their 10 hours mattered.

---

## DESIGN MANIFESTO

FRAMEWAR is a game about making things that matter inside a system that rewards making things that sell. Every mechanic serves that tension. The Greenlight Table is where you choose between your heart and your wallet. The Production Pipeline is where you discover that creative vision and practical constraints are the same conversation. The Talent Engine is where you learn that brilliant people are also difficult people. The Tech Tree is where you decide whether to chase the future or defend the past. The Box Office Gauntlet is where the market tells you whether you were right.

The game asks one question across ten hours: **What kind of studio did you build?**

Not "how much money did you make" -- though money is survival. Not "how many awards did you win" -- though awards are validation. The question is about identity. When you look at the filmography shelf at the end of the campaign -- eight or ten films, each one a scar or a trophy -- what story does it tell? Did you build a studio that made people feel something? Did you build a studio that paid its artists and kept its promises? Did you build a studio that took a risk when it counted?

The shelf is the answer. The shelf is the score. The shelf is the game.

---

*Designed by REED. Every number in this document is a starting point for playtesting, not a final answer. The formulas will change. The balance will shift. The decision density will be tuned. But the core loop -- greenlight, shepherd, harvest, reckon -- is the spine. If that spine holds, everything else is iteration. If it doesn't, we start over. We never say "we'll figure out the fun later."*
