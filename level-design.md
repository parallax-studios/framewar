# FRAMEWAR -- Level Design Document

**Designer**: GRID
**Version**: 1.0
**Date**: 2026-02-07
**Status**: Complete First Pass

---

## GRID SPEAKS

I don't design menus. I design spaces where decisions happen.

Every room in this studio is a sightline. Every corkboard is a breadcrumb. Every threshold teaches the player where to look next. The player isn't navigating a UI -- they're walking through their creative life. By hour ten, they should know this building like their own apartment. They should have a favorite corner. They should remember the first time they walked into the screening room and saw their film on the big screen.

The studio is the level. The pipeline is the path. The filmography shelf is the finish line.

Let's build it.

---

## 1. SPATIAL PHILOSOPHY: THE DIEGETIC STUDIO

### 1.1 Core Principle

**The entire game exists in physical space. No abstract menus. No floating UI panels. The studio IS the interface.**

Where does the player LOOK? They look at their work -- pinned to corkboards, displayed on monitors, projected on screens. They look at their people -- animators at desks, directors in meeting rooms, voice actors in recording booths. They look at the physical accumulation of their decisions -- the filmography shelf, the Oscar case, the render farm blinking through another all-nighter.

What does this teach? It teaches presence. The player doesn't feel like they're managing spreadsheets. They feel like they work here.

### 1.2 Camera System

**Perspective**: Isometric view, 45-degree angle, inspired by Unpacking and Two Point Hospital. The camera looks down at the studio floor from a gentle overhead angle. The player sees multiple rooms simultaneously when zoomed out, creating a readable spatial overview. Zoom in and the camera focuses on a single workspace with readable detail -- storyboard panels, monitor contents, character animations at desks.

**Navigation**: The player moves through the studio in three ways:
1. **Free Camera Pan**: Click-drag or WASD to slide the camera across the studio floor. No camera rotation -- the isometric angle is fixed. Consistency of perspective means the player builds a mental map.
2. **Room Jump**: Click on a room icon in the studio HUD (a minimal overlay showing room silhouettes) to instantly pan the camera to that space. Think of it as "I need to check the render farm" -- click, camera slides there in 0.4 seconds.
3. **Notification Summons**: When an event requires attention (a decision point surfaces, a production phase completes), a visual ping appears in 3D space over the relevant room. Click the ping and the camera pans there. The player learns to read the studio spatially -- "that ping is in the storyboard room, must be a director request."

**Zoom**: Mouse wheel or hotkeys. Three zoom levels:
- **Studio Overview**: See the entire studio floor at once. Used for strategic assessment and quarterly planning.
- **Room Focus**: See 2-3 rooms in detail. Used for active management and decision-making.
- **Desk Detail**: See individual workstations, monitor screens, pinned documents. Used for reading content and flavor.

Where does the player LOOK when they first load the game? The camera starts at Studio Overview, centered on the filmography shelf in the lobby. The shelf is empty. That emptiness is the hook -- the player's first question is "how do I fill that?"

### 1.3 Time System and Pacing Control

**Time Flow**: The game runs in real-time with pause, inspired by RimWorld and Oxygen Not Included. Time flows in quarters (3 in-game months = roughly 2-3 minutes of real time at default speed). The player can pause, play at 1x speed, or accelerate to 3x speed.

**Auto-Pause Triggers**: The game auto-pauses on high-stakes decision points -- greenlight table evaluations, production phase gates, box office results, talent loyalty crises, awards announcements. Low-stakes events (routine resource allocation, minor animator assignments) do not pause -- they appear as notifications the player can address at their pace.

Where's the pacing? Quarters are the heartbeat. The player learns the rhythm: play a quarter, events surface, pause and address them, advance the next quarter. It's a breath cycle. Experienced players accelerate through routine quarters and slow down for critical moments. That mastery of pacing IS the mastery of the game.

---

## 2. THE STUDIO FLOOR: SPATIAL LAYOUT AND FLOW

### 2.1 Starting Configuration (Era 1: 1995-1998)

The player begins with a small studio: six rooms arranged in a compact L-shape. Total footprint: roughly 40m x 30m.

**Room List**:
1. **Lobby and Filmography Shelf** (entrance, always visible when zoomed out)
2. **Greenlight Office** (where the player sits, where pitches arrive)
3. **Storyboard Room** (development and pre-production work)
4. **Animation Floor** (animator workstations, 6 desks initially)
5. **Render Farm** (small, 12 processing units)
6. **Screening Room** (dailies review, test screenings, box office results)

**Spatial Arrangement**:

```
                  NORTH
        +-----------+-----------+
        | RENDER    | ANIMATION |
        | FARM      | FLOOR     |
        +-----------+-----------+
        | STORYBOARD| SCREENING |
        | ROOM      | ROOM      |
        +-----------+-----------+
        | GREENLIGHT|           |
        | OFFICE    | LOBBY +   |
        |           | SHELF     |
        +-----------+-----------+
              ENTRANCE (SOUTH)
```

**Flow Logic**: The player enters from the lobby (bottom). The filmography shelf is the first thing they see -- their legacy, currently empty. The greenlight office is immediately adjacent (left) -- where work begins. From the office, the production pipeline flows LEFT-TO-RIGHT and BOTTOM-TO-TOP: concepts greenlit in the office move to the storyboard room (northwest), then to animation floor (northeast), supported by the render farm (north), and finally screened in the screening room (east). The spatial flow mirrors the production pipeline.

What does this teach? It teaches the pipeline without a tutorial. The player's eye follows the path from greenlight to release by moving through the space. Every film is a journey across the studio floor.

### 2.2 Expanded Configuration (Era 2-3: 1999-2005)

As the studio grows (funded by successful releases and unlocked through $20M studio expansion investments), new wings are added. The studio expands to the north and west, creating a larger compound.

**New Rooms** (added across Eras 2-3):
7. **Voice Recording Booth** (voice casting, recording sessions)
8. **Post-Production Suite** (lighting, effects, sound mixing)
9. **Story Room** (dedicated space for story artists, separated from storyboarding)
10. **Marketing Department** (trailer creation, festival prep, campaign management)
11. **Executive Conference Room** (rival studio intel, distribution deals, crisis meetings)
12. **Expanded Render Farm** (doubles capacity to 30+ units)
13. **Second Animation Floor** (allows simultaneous multi-film production)

**Expanded Spatial Arrangement** (Era 3):

```
                      NORTH
    +--------+--------+--------+--------+
    | STORY  | RENDER | RENDER | ANIM   |
    | ROOM   | FARM   | FARM   | FLOOR  |
    |        | (EAST) | (WEST) | (EAST) |
    +--------+--------+--------+--------+
    | EXEC   |STORYBD | POST-  | SCREEN |
    | CONF   | ROOM   | PROD   | ROOM   |
    +--------+--------+--------+--------+
    | MKT    |GREENLT | VOICE  | ANIM   |
    | DEPT   | OFFICE | BOOTH  | FLOOR  |
    |        |        |        | (WEST) |
    +--------+--------+--------+--------+
    |        | LOBBY + FILMOGRAPHY      |
    |        | SHELF                    |
    +--------+--------------------------+
                  ENTRANCE (SOUTH)
```

**Flow Evolution**: The expanded studio creates multiple simultaneous flow paths. Two films can be in production at once, each with their own animation floor. The render farm is now centrally located, serving both animation floors. The voice booth and post-production suite slot into the middle phases of the pipeline. Marketing is near the entrance -- films exit through marketing to release.

What does this teach? It teaches complexity management. The player who could track one film by glancing left-to-right must now track two or three films across a larger space. The studio's growth mirrors the player's cognitive load -- and their mastery. A veteran player pans across the floor and reads the entire state in 3 seconds: "TIDEWALKER is in animation, FOLDED is in storyboards, SIGNAL is in post-production, render farm at 60%, no crises."

### 2.3 Endgame Configuration (Era 4-5: 2006-2010)

By late game, the studio is a sprawling production facility. Optional expansions add prestige and capacity.

**Optional Late-Game Rooms**:
14. **Awards Campaign Office** (Oscar campaign management, festival strategy)
15. **Franchise Planning Room** (sequel development, IP management)
16. **Hybrid Production Studio** (integrated 2D/CG workspace for hybrid approach)
17. **Archive and Legacy Wing** (past film materials, concept art library, retrospective prep)

The player doesn't build all of these -- they choose based on their studio identity. An ARTIST-leaning studio builds the Archive. An EXECUTIVE-leaning studio builds Franchise Planning. The spatial layout becomes a physical manifestation of the player's choices.

---

## 3. ROOM-BY-ROOM BREAKDOWN: PURPOSE, ENCOUNTERS, BREADCRUMBS

### 3.1 The Lobby and Filmography Shelf

**PURPOSE**: Emotional anchor. This is the player's legacy made visible.

**LAYOUT**:
- The lobby is a two-story atrium with warm lighting (always the warmest room in the studio, contrast against the cool render farm).
- The filmography shelf occupies the north wall: a floor-to-ceiling display showing released films as physical boxes (think DVD cases but stylized, gold-trimmed).
- Each film shows its poster art, title, release year, total gross, Projector Score, and any awards won (Oscar statuettes rendered as small golden models on the shelf).
- A seating area (couches, coffee table) in front of the shelf -- during certain events, characters appear here for conversations.

**KEY ENCOUNTERS**:
- **First Visit (Tutorial)**: The player stands in the empty lobby. A voiceover (or text prompt styled as internal monologue) says: "An empty shelf is a promise. What story will you tell?" The camera pans to the greenlight office. The first breadcrumb.
- **Post-Release Moments**: After each film releases, a cutscene (or brief animated moment) shows the film's box being placed on the shelf. The player hears the sound of the case sliding into place. If the film won awards, the Oscar statuette appears with a soft golden glow. This is the dopamine hit -- the tangible reward.
- **Mid-Campaign Reflection (Era 3)**: If the player has 4+ films on the shelf, a character event triggers here. Ruth, Dani, or Marlowe (depending on relationship) sits on the couch and comments on the filmography. "You've built something. Can you see it?" The NPC's dialogue adapts to the shelf's composition -- all sequels, all originals, a mix, awards, flops.
- **Endgame Retrospective (Final Scene)**: The game's final moment is in this room. The camera slowly pans across the shelf, lingering on each film. Procedurally generated narration reflects on the studio's legacy. The player sees the full arc: the first modest film, the breakout hit, the risky passion project, the franchise, the Oscar winner, the final statement. The shelf tells the story.

**BREADCRUMBING**: The shelf is always visible when the player is zoomed out to Studio Overview. It's the visual center. New players are drawn to it because it's empty and beautiful -- it demands to be filled. Veteran players return to it between productions to see their legacy accumulate. It's the finish line that's always in sight.

**SIGHTLINES**: From the lobby, the player can see into the greenlight office (west) and glimpse the storyboard room beyond. The spatial language says: "Start here, then go there." The flow is intuitive.

---

### 3.2 The Greenlight Office

**PURPOSE**: The decision hub. Where every film begins.

**LAYOUT**:
- A medium-sized office with a large desk (the player's desk, though the player is never embodied as a character).
- The north wall is dominated by a massive corkboard (3m x 2m) where film pitches are pinned as physical concept cards.
- Each concept card is a stylized document showing the film's logline, concept art thumbnail, and visible attribute icons (ORIGINALITY, AUDIENCE BREADTH, TECHNICAL AMBITION, SEQUEL POTENTIAL displayed as 1-10 dots in colored circles).
- A calendar on the east wall shows the current quarter/year and upcoming release windows.
- Bookshelves with reference materials (dusty, lived-in).
- A window overlooking a stylized LA skyline (palm trees, golden hour light in daytime, city lights at night).

**KEY ENCOUNTERS**:
- **Pitch Arrival Events**: Each quarter, 1-3 new concept cards appear on the corkboard with a soft "pin" sound effect. The player clicks on a card to read the full pitch -- a pop-up window styled as an unfolding document.
- **Greenlight Decision**: Dragging a concept card from the corkboard to the desk initiates the greenlight sequence. A form appears: assign Director (dropdown of available talent), set budget (slider), choose release window (calendar interaction), select technology approach (2D/CG/Hybrid buttons). Confirming the greenlight triggers a satisfying "stamp" animation -- a greenlight stamp comes down on the document. The concept card is removed from the corkboard and appears on the Production Pipeline Board (in the adjacent storyboard room). The spatial connection is immediate: greenlighting sends the film next door.
- **Rival Intel Briefings**: Periodically, a document appears on the desk: a "competitive intelligence report" showing rival studios' upcoming releases. This is flavor and strategic information -- when is Luminos releasing their prestige film? When is TitanToon's sequel dropping? The player uses this to time their own release windows.
- **Character Meetings**: When a Director wants to pitch a film, or when a talent loyalty crisis occurs, that character appears in the office (standing on the other side of the desk). The conversation interface is spatial: the character's portrait, dialogue, and choice options appear as diegetic elements (speech bubbles, thought balloons, decision cards on the desk).

**BREADCRUMBING**: The corkboard is the game's core loop generator. New pitches arriving is the "ding" that says "there's something to do." The corkboard is always visible when the player is in this room, and new cards have a subtle glow/pulse to draw the eye. The player learns: "Check the corkboard every few quarters."

**PACING**: Early game, the player spends a lot of time here -- reading pitches, agonizing over greenlight decisions. Mid-game, they become faster -- they've learned to read the attributes and trust their instincts. Late game, they scan the corkboard for the one pitch that matters -- the film that will define their legacy.

**SIGHTLINES**: The west-facing window provides environmental storytelling. Early game (1995), the skyline is less developed. Late game (2010), it's denser, more lit. The passage of time is visible outside the window. Additionally, through the north doorway, the player can see into the storyboard room and glimpse the Production Pipeline Board -- the next step is always visible.

---

### 3.3 The Storyboard Room

**PURPOSE**: Where story is born. Development and pre-production phase management.

**LAYOUT**:
- A large, warmly lit room with multiple corkboards mounted on walls (at least 6 separate boards, each representing a different film or phase).
- The west wall holds the **Production Pipeline Board** -- a massive horizontal timeline showing all active films as cards moving through six columns: DEV | PRE-PROD | PROD | POST | MKT | RELEASE. This is the game's strategic spine, always visible, always updated. Each film card shows its title, assigned Director, current phase, quarters remaining in phase, and a small progress bar.
- The other walls are covered with storyboard panels -- drawings pinned in sequence, representing the current films in development/pre-production. These update dynamically as the player progresses through phases. Early in Development, the boards are sparse (a few rough sketches). Later, they're filled (complete animatics).
- Animator desks (2-3) occupied by story artists working on boards.
- A large central table for story meetings (used during event cutscenes).

**KEY ENCOUNTERS**:
- **Development Phase Decisions**: When a film is in Development, clicking on its card in the Production Pipeline Board zooms the camera into this room and highlights the relevant storyboard panels. The player is presented with story outline choices (3 options generated by the Story Artist, each showing bias toward different DNA attributes). Selecting an outline updates the storyboard panels on the wall -- new drawings appear, the player sees the film taking shape.
- **Tone Calibration**: A sliding interface appears over the central table -- two axes (Light/Dark, Grounded/Fantastical). Adjusting the tone shifts the visual style of the concept art pinned to the boards. This is tactile feedback: the player's decision has immediate visual impact.
- **Storyboard Review (Pre-Production)**: The Director presents an animatic (shown as a sequence of panels with playback icons). The player clicks through the animatic (essentially a slideshow of storyboard art with limited animation/camera moves). At the end, three choices: Approve (green thumbtack animation, proceed), Request Revision (yellow thumbtack, cost time/money, improve STORY DEPTH), Override Director (red thumbtack, preserve schedule, risk morale damage). The thumbtacks appear physically on the board.

**BREADCRUMBING**: The Production Pipeline Board is the player's compass. It is always visible on the west wall of this room. When a film's card pulses (indicating a decision point), the player knows to click it. The pipeline board teaches temporal awareness: "TIDEWALKER is two quarters from finishing production. FOLDED is entering pre-production. I need to allocate animators soon." The spatial representation of time makes the three-to-four-year pipeline legible.

**PACING**: Early game, one film on the board. Mid-game, three films scattered across phases. Late game, the board is a symphony of simultaneous progress -- the player pans across it like a conductor reading a score.

**SIGHTLINES**: From this room, the player can see into the animation floors (north/east) and the greenlight office (south). The storyboard room is the hub -- most player time is spent here because the Production Pipeline Board is the central interface. The room's central position in the studio layout is intentional.

---

### 3.4 The Animation Floor(s)

**PURPOSE**: Where the work happens. Production phase management.

**LAYOUT** (per floor):
- 6-12 animator desks arranged in rows, each desk with a monitor, reference materials, and personal touches (photos, figurines, coffee mugs).
- Each animator is represented as a stylized character at their desk, actively working (subtle idle animations: drawing on tablet, checking monitors, stretching, talking to neighbor).
- Monitors show the work-in-progress -- rotating clips of animation tests, wireframe models, rendered frames. Early in production, monitors show rough blockouts. Late in production, they show polished footage.
- A wall-mounted display shows the current film's production status: quarters remaining, animator team composition (names + QUALITY/SPEED stats), render farm allocation percentage, and a "dailies quality" meter (visual approximation of current ANIMATION QUALITY trajectory).
- Whiteboards with schedules, notes, and occasional doodles (flavor).

**KEY ENCOUNTERS**:
- **Animator Assignment**: Clicking on a film in Production phase opens an animator assignment interface. Available animators appear as portrait cards (showing name, STYLE, QUALITY, SPEED, MORALE). The player drags animator cards to assignment slots on the film's production board. Assigned animators physically appear at desks in this room, and their monitors start showing footage from the assigned film. The spatial feedback reinforces the decision: "I assigned Dani to TIDEWALKER, and now I see her at desk 3 working on it."
- **Dailies Review**: Each quarter during Production, a "dailies available" notification pings this room. Clicking it triggers a mini-cutscene: the camera zooms to a desk, a monitor plays a 5-10 second animation clip (procedurally selected to reflect current quality trajectory), and the player is prompted to evaluate. If quality is below target, options appear: Crunch (push harder), Add Animators (cost increase), Accept Trajectory (lock in current path).
- **Director Deviation Requests**: The assigned Director's portrait appears in the room (standing near the central aisle) with a speech bubble: "I want to add a dream sequence to Act 2. It'll cost us a quarter and $3M, but it'll make the film sing." The player's choice (Approve, Deny) updates Director morale and Film DNA scores. The spatial context matters: the Director is standing in the room where their vision is being executed. The player feels the weight of the conversation.
- **Crunch and Morale Crises**: If animators are in crunch, their desk animations change -- they slump, rub eyes, work more frantically. Morale meters (small icons above desks, color-coded green/yellow/red) become visible. If an animator quits, their desk empties with a brief animation (they pack up, walk off-screen). The empty desk remains visible until the player hires a replacement. The absence is spatial and painful.

**BREADCRUMBING**: The wall display is the breadcrumb -- it shows at a glance which films are in production and whether they're on track. Pulsing alerts appear above specific desks when a decision is needed (dailies ready, animator morale critical, render issue).

**PACING**: Production is the longest phase (3-5 quarters). The animation floor is where the player spends most mid-game time. The room evolves over the course of a production: from empty desks to full team to polished footage on monitors. Watching this evolution IS the pacing -- the player sees the film being made.

**SIGHTLINES**: The animation floors have windows overlooking the render farm (if adjacent). The player sees the render farm monitors flickering in parallel -- a visual reminder that animation and rendering are connected systems. The spatial relationship teaches the pipeline.

---

### 3.5 The Render Farm

**PURPOSE**: The technical heart. Renders animation, visualizes technology investment.

**LAYOUT**:
- A dimly lit room (coolest color temperature in the studio, contrast with the warm storyboard room).
- Rows of server racks with monitors showing render progress bars, frame previews, and processing status.
- Each active film in Production/Post has a dedicated monitor cluster showing real-time render progress (current frame, estimated completion time, render queue).
- A central control terminal where the player allocates render farm capacity across films (if multiple productions are active).
- Occasional flickering lights, fan hum sound design -- this room feels alive and mechanical.

**KEY ENCOUNTERS**:
- **Render Allocation**: When multiple films are in production, clicking the central terminal opens a resource allocation interface. The player assigns render farm capacity (as percentages, must total ≤100%) to each active film. Over-allocating (above 60% for extended periods) increases crisis risk.
- **Render Farm Crises**: If over-allocated, a crisis event triggers: monitors flash red, an error alert appears. Options: Pay for emergency hardware fix ($2M), Accept delay (+1 quarter), or Reduce capacity (slow progress on all films). The spatial presentation -- flashing red monitors, alarms -- makes the crisis visceral.
- **Technology Showcases**: When a new tech tree node completes (e.g., Advanced Fur/Hair), a brief cutscene plays in this room: a monitor displays a render test showcasing the new capability (photorealistic fur, fluid simulation, etc.). This is the payoff for tech investment -- the player sees the breakthrough.

**BREADCRUMBING**: Monitors are color-coded: green (on schedule), yellow (behind schedule), red (crisis). A glance at the render farm tells the player the technical health of all productions. The render farm is the game's heartbeat monitor.

**PACING**: The render farm runs passively -- the player doesn't micro-manage it unless a crisis occurs. It's a space the player checks periodically ("How's the render looking?") rather than inhabits constantly. The rhythm of checking it becomes meditative.

**SIGHTLINES**: The render farm has a window into the animation floor (if adjacent). The player sees animators working while processors churn. The connection is spatial and thematic: human creativity + machine processing = film.

---

### 3.6 The Screening Room

**PURPOSE**: Review, release, and reckoning. Where the player sees results.

**LAYOUT**:
- A small theater with tiered seating (12-15 seats).
- A large projection screen on the north wall.
- The room is dark except for the screen glow and subtle floor lighting.
- Seats are occasionally occupied by NPCs during specific events (directors, story artists, test audiences).

**KEY ENCOUNTERS**:
- **Dailies Screenings**: During Production/Post-Production, clicking a "watch dailies" notification brings the player here. The screen plays a 10-20 second clip of animated footage (procedurally selected based on current film progress and quality). This is the player's first look at the film they're making. The footage quality reflects animator assignments, tech tree state, and production decisions. After the clip, an evaluation prompt appears.
- **Test Screening (Post-Production)**: If the player chooses to run a focus test, this room fills with NPCs (stylized silhouettes representing test audience). The screen shows the film's "projected audience score" as a large number (e.g., 62/100) with noisy error bars (+/- 15). Based on the score, the player chooses final adjustments (re-cut for humor, add crowd-pleasing ending, leave as-is). The test audience's reactions (applause, polite silence, walkouts) are shown spatially -- NPCs stand and leave if the score is below 40.
- **Box Office Gauntlet (Release Phase)**: This is the most dramatic use of the screening room. When a film releases, the player is brought here. The screen displays:
  - **Week 1**: Opening weekend numbers with animated box office charts, critic review aggregation (Projector Score reveal with animated score wheel), audience score.
  - **Weeks 2-4**: Weekly revenue tracking, drop-off curves, competitor releases (rival films appear on the chart as colored bars).
  - The player sits in the audience. The pacing is deliberate -- each week's results appear with a 5-10 second delay, building tension. The player can fast-forward after the first few films, but the first release is a full, slow, agonizing/exhilarating experience.
- **Awards Ceremony (if Oscar-eligible)**: If a film is nominated for Best Animated Feature, the screening room transforms. The screen shows a stylized Oscar ceremony -- the envelope, the presenter, the pause, the announcement. If the player wins, the screen shows the acceptance speech (delivered by the Director, procedurally generated text thanking the team). The moment is punctuated by applause sound design. The player then sees the Oscar statuette appear on the filmography shelf.

**BREADCRUMBING**: The screening room is the resolution space -- every production arc ends here. The player learns: "When a film is finished, I go to the screening room to see what I made."

**PACING**: The screening room is a pacing valve. It forces the player to slow down and watch outcomes unfold. The box office gauntlet's week-by-week reveal creates a rhythm: anticipation, reveal, reaction, next week. By the third or fourth release, experienced players can accelerate, but the ritual remains.

**SIGHTLINES**: The screening room has no windows (thematically appropriate -- it's a sealed space, focused entirely on the screen). Entering it is a transition from the busy production floor to a moment of stillness and judgment.

---

### 3.7 Supporting Rooms (Post-Production, Voice Booth, Marketing, Etc.)

**Post-Production Suite**:
- Purpose: Lighting, effects, sound mixing decisions.
- Layout: Workstations with color grading monitors, sound mixing boards, effects preview screens.
- Key encounter: Budget allocation for effects/sound, with preview clips showing before/after comparisons.

**Voice Recording Booth**:
- Purpose: Voice actor casting and recording.
- Layout: Soundproof booth visible through glass, recording console.
- Key encounter: Audition playback (procedurally generated voice samples), chemistry preview (if casting multiple actors, a "read together" test shows chemistry modifier).

**Marketing Department**:
- Purpose: Trailer strategy, festival submissions, marketing budget allocation.
- Layout: Desks with marketing materials, posters on walls, a wall-mounted calendar showing release schedule and festival dates.
- Key encounter: Trailer emphasis choice (which DNA attribute to emphasize), festival submission interface.

Each supporting room follows the same spatial logic: purpose is clear from layout, decisions are diegetic (appear as objects in space), and breadcrumbs (notifications, pings) guide the player when action is needed.

---

## 4. FLOW DESIGN: NAVIGATING THE PRODUCTION PIPELINE

### 4.1 The Greenlight-to-Release Path

**The player's primary flow is spatial**. A film's journey through production is a journey across the studio floor. Let's trace a single film's spatial path:

**Phase 1: Greenlight** → Player is in the Greenlight Office. Concept card pinned on corkboard. Player drags it to desk, fills out greenlight form, stamps it. Card disappears from corkboard and appears on the Production Pipeline Board in the Storyboard Room (visible through the doorway).

**Phase 2: Development** → Player pans to Storyboard Room. Clicks the film's card on the Pipeline Board. Story outline choices appear over the central table. Player selects. Storyboard panels start appearing on the walls. Quarters pass. Development completes. Film card slides from DEV column to PRE-PROD column on the Pipeline Board.

**Phase 3: Pre-Production** → Still in Storyboard Room. Voice Casting decision triggers -- a notification pings the Voice Booth (visible to the east). Player pans to Voice Booth, auditions actors, casts roles. Returns to Storyboard Room for storyboard review. Director presents animatic. Player approves/revises. Pre-production completes. Film card slides to PROD column.

**Phase 4: Production** → Player pans to Animation Floor (north). Assigns animators. Animators appear at desks, monitors show work. Quarters pass. Dailies notifications ping the Screening Room. Player pans to Screening Room, watches clips, makes crunch/resource decisions. Render Farm (visible to the west) shows progress bars advancing. Production completes. Film card slides to POST column.

**Phase 5: Post-Production** → Player pans to Post-Production Suite. Allocates effects/sound budget. Preview clips show improvements. Post completes. Film card slides to MKT column.

**Phase 6: Marketing** → Player pans to Marketing Department. Sets marketing budget, chooses trailer emphasis, locks release date. Checks rival calendar (visible on wall). Marketing completes. Film card slides to RELEASE column.

**Phase 7: Release** → Player is summoned to Screening Room. Box office gauntlet plays out. Results appear. Film card disappears from Pipeline Board. Camera pans to Lobby. Film appears on the Filmography Shelf with a satisfying "slide into place" animation.

**What does this flow teach?** It teaches the pipeline as a spatial journey. The player doesn't read the pipeline in a flowchart -- they walk it. By the third film, the player doesn't need tutorials. They know: "Film is greenlit, next I go to storyboards, then animation, then screening." The space is the teacher.

### 4.2 Multi-Film Flow (Mid-to-Late Game)

When managing 2-3 simultaneous productions, the flow becomes orchestration:

- **Camera panning becomes strategic**. The player scans across the studio: "TIDEWALKER is in animation, FOLDED is in development, SIGNAL is in marketing. Render farm is at 75% -- I need to check for overages. Storyboard room has a pulsing notification -- FOLDED needs a tone decision. Animation floor (west) has a red morale alert -- someone is about to quit."

- **The Production Pipeline Board becomes the master view**. The player zooms to Storyboard Room, looks at the Pipeline Board, reads the state of all films at once. This is the game's strategic map.

- **Notifications teach prioritization**. Green pings (routine decisions) can wait. Yellow pings (time-sensitive decisions) should be addressed soon. Red pings (crises) demand immediate attention. The player learns to triage by color and location.

**Pacing curve across a campaign**:
- Hours 1-2: One film, slow pace, learning the spaces.
- Hours 3-5: Two films, moderate pace, learning to juggle.
- Hours 6-10: Three films, fast pace, mastery. The player pans across the studio like a conductor, addressing decisions in seconds.

The pacing curve IS the difficulty curve. The game doesn't add complexity through new mechanics -- it adds complexity through tempo and simultaneity.

---

## 5. ENCOUNTER DESIGN: DECISION POINTS AS SPATIAL MOMENTS

### 5.1 High-Stakes Decisions

Every major decision in FRAMEWAR is a **spatial encounter** -- the player goes to a specific room, the camera frames a specific moment, the decision is presented diegetically.

**Example: The Director Deviation Request (Production Phase)**

- **Setup**: TIDEWALKER is in Production, quarter 3/5. Assigned Director is Marlowe Voss (VISION 9, EGO 8). The player is panning across the studio.
- **Trigger**: A yellow notification ping appears above the Animation Floor (east).
- **Approach**: Player clicks the ping. Camera pans to Animation Floor (east), zooms to Room Focus level.
- **The Encounter**: Marlowe's character portrait appears standing in the central aisle between animator desks. His dialogue appears in a diegetic speech bubble (stylized as a handwritten note):
  - *"I need to add a sequence. The lighthouse keeper has a memory of his daughter -- it's the emotional core of Act 2. It'll cost us three weeks and $3 million. But without it, the film is hollow."*
- **Decision Space**: The player's desk (in the Greenlight Office) virtually appears in the foreground as a UI element. Three decision cards appear on the desk:
  - **APPROVE**: "+1 quarter, +$3M, HEART +0.5, Director morale +10" (green card)
  - **NEGOTIATE**: "Reduce scope: +0.5 quarters, +$1.5M, HEART +0.2, Director morale +3" (yellow card)
  - **DENY**: "No cost, Director morale -15, risk of HEART cap at 6" (red card)
- **Resolution**: Player drags a card to a "decision stamp" icon. The choice is locked with a stamp animation. Marlowe reacts (nods if approved, frowns if denied, walks away). The encounter ends. Production continues.

**Why is this spatial?** Because the player is in the room where the work happens. Marlowe is standing among the animators who will execute his vision. The decision feels real because the context is visible. The player isn't clicking through abstract menus -- they're having a conversation in a workspace.

### 5.2 Crisis Encounters

Crises are the game's most dramatic spatial moments.

**Example: The Animator Loyalty Crisis**

- **Setup**: Dani Chen (legendary animator, QUALITY 9) has been assigned to TIDEWALKER for 4 quarters. Morale is at 35 (low, due to crunch). The player is mid-quarter advance.
- **Trigger**: A red notification ping appears above Dani's desk in the Animation Floor (west).
- **Approach**: Player clicks ping. Camera zooms to Dani's desk. Dani's character stands up from her desk (animated), turns to camera.
- **The Crisis**: Dani's dialogue appears:
  - *"Luminos made me an offer. $220K, no crunch, a lead role on their next film. I love what we're building here, but I can't keep working like this. Match their offer and promise me the next film is different, or I'm gone."*
- **Decision Space**: Options appear as cards on Dani's desk:
  - **MATCH OFFER + PROMISE**: "Salary increases to $220K/year, commit to no crunch on next film, Dani stays, loyalty +20" (costs budget, constrains future)
  - **MATCH OFFER ONLY**: "Salary increases to $220K/year, Dani stays short-term, loyalty +5, risk of departure next crisis" (buys time)
  - **LET HER GO**: "Dani leaves immediately, TIDEWALKER loses -1 ANIMATION QUALITY, Luminos gains Dani as talent, she appears in their future films as competitor" (painful but survivable)
- **Resolution**: Player chooses. If Dani stays, she sits back down (visible relief animation). If she leaves, she packs her desk (brief animation: collects belongings, waves goodbye, walks off-screen), and the desk remains empty. The camera lingers on the empty desk for 2 seconds (silence). The absence is spatial. The player feels it.

**Why is this a crisis?** Because the player has seen Dani working for 4 quarters. Her desk is familiar. Her contributions to TIDEWALKER are visible on her monitor. Losing her isn't losing a stat -- it's losing a person the player has watched work.

### 5.3 Narrative Encounters

**Example: Ruth's Final Day (2D Division Closure)**

- **Setup**: The player has decided to close their 2D animation division (2003, after the market has turned). Ruth Alvarez is the studio's last 2D art director.
- **Trigger**: After confirming the closure decision, the camera automatically pans to the 2D wing (if it exists as a separate space, or to Ruth's desk in the Animation Floor).
- **The Encounter**: Ruth is alone. The 2D desks are empty (other 2D animators have already been laid off). Ruth is packing her desk. The camera is close (Desk Detail zoom). The player sees her picking up a pencil (a Blackwing 602, rendered with care), looking at it, placing it in her jacket pocket. No dialogue. Just the action. Environmental storytelling.
- **Optional Dialogue**: After a 3-second pause, Ruth turns to camera (breaking the fourth wall slightly, as if she knows the player is watching). Text appears:
  - *"Nineteen years of drawings, in two pencils. You made the smart choice. Just know what it cost."*
- She walks off-screen. The desk remains empty for the rest of the game. If the player later pans to this space, the empty desk is still there -- a scar on the studio floor.

**Why is this powerful?** Because it's spatial and silent. The player doesn't choose dialogue options. They witness. The empty desks, the pencil, the slow walk away -- these are spatial beats that hit harder than any scripted monologue.

---

## 6. BREADCRUMBING STRATEGY: GUIDING WITHOUT HAND-HOLDING

### 6.1 Visual Language

FRAMEWAR uses a consistent visual language to guide player attention without UI clutter:

**Notification Pings** (3D markers in space):
- **Green Ping**: Routine decision (e.g., "dailies ready," "quarterly resource allocation"). No urgency. Can be addressed at player's convenience.
- **Yellow Ping**: Time-sensitive decision (e.g., "phase gate approaching," "Director request"). Should be addressed within 1-2 quarters.
- **Red Ping**: Crisis (e.g., "animator quitting," "render farm failure," "budget overrun"). Requires immediate attention. Game auto-pauses when red pings appear.

**Color Coding** (consistent across all UI):
- **Gold** (Prestige): Awards, quality indicators, high-VISION directors, prestige pitches.
- **Green** (Commercial): Revenue, box office, profitable decisions.
- **Blue** (Technical Innovation): Tech tree, render farm, animation quality.
- **Purple** (Artistic Courage): High-ORIGINALITY films, 2D innovations, risky creative choices.
- **Red** (Crisis): Overruns, failures, critical morale.

**Spatial Breadcrumbs**:
- **Lit Doorways**: When a decision is needed in an adjacent room, the doorway to that room glows faintly (subtle golden outline). The player learns: "Something's happening through that door."
- **Pulsing Objects**: The Production Pipeline Board's film cards pulse when a phase decision is needed. The greenlight office corkboard glows when new pitches arrive. The filmography shelf glows after a film releases (drawing the player to see the new addition).
- **Character Placement**: NPCs appear in rooms where decisions involving them occur. If a Director wants to talk, they appear in the production space. If a rival studio head sends an intel report, their portrait appears briefly in the Executive Conference Room. The player learns to read the space: "Marlowe is in the storyboard room -- he must have feedback on the animatic."

### 6.2 Teaching Through Repetition and Ritual

The game teaches through ritual repetition. By the third film, the player has internalized the flow:

**The Greenlight Ritual**:
1. New concept cards appear on corkboard (green ping, "new pitches available").
2. Player reads concepts, evaluates attributes.
3. Player drags chosen concept to desk, fills greenlight form.
4. Stamp animation. Film appears on Pipeline Board.

By film 3, this takes 30 seconds. By film 6, it takes 10 seconds. The space has taught the player the rhythm.

**The Release Ritual**:
1. Film enters Release phase.
2. Player is summoned to Screening Room (auto-camera pan).
3. Box office gauntlet plays (4 weeks, results appear).
4. Camera pans to Lobby. Film appears on shelf.

By release 3, the player knows the ritual. The anticipation is built into the spatial journey: "I'm about to see what I made."

### 6.3 The First Hour: Tutorial Without Tutorializing

**Minute 0-5**: Player loads game. Camera starts at Lobby (filmography shelf, empty). Text prompt: *"An empty shelf is a promise."* Camera pans to Greenlight Office. A single concept card is already pinned on the corkboard (pre-placed for tutorial pacing). Player clicks it, reads pitch.

**Minute 5-10**: Player greenlights first film (simplified form: only budget and Director choice, tech approach auto-set to basic CG). Stamp animation. Camera pans to Storyboard Room. Film card appears on Pipeline Board in DEV column. Text prompt: *"Development begins. Your story artists are working."*

**Minute 10-20**: Quarters advance (accelerated pace for tutorial). Development completes. Film card slides to PRE-PROD. Notification pings Storyboard Room. Player clicks. Storyboard review encounter. Player approves. Pre-production completes.

**Minute 20-30**: Film enters Production. Camera pans to Animation Floor. Tutorial highlights animator assignment. Player assigns 3 animators (simplified choice, no optimization required). Production advances (accelerated). Dailies notification. Player watches first clip in Screening Room.

**Minute 30-40**: Production completes. Post-production (simplified: one budget slider for effects). Marketing (simplified: budget only). Film enters Release.

**Minute 40-50**: Box office gauntlet (full experience, not accelerated). Player watches opening weekend, week-by-week results, reviews, awards eligibility. First film is designed to be modestly successful ($120M gross, Projector Score 68, profitable but not groundbreaking).

**Minute 50-60**: Camera pans to Lobby. Film appears on shelf. Text prompt: *"One down. What's next?"* Camera pans to Greenlight Office. New concept cards have appeared. Tutorial ends. The player is now in the loop.

**What did the tutorial teach?** It taught the spatial flow by walking the player through it once. No text walls. No abstract explanations. Just: "Do this, then go here, then this happens." The space is the teacher.

---

## 7. DIFFICULTY CONSIDERATIONS: SPATIAL AND TEMPORAL PRESSURE

### 7.1 Difficulty Axes

FRAMEWAR's difficulty is not about reflexes or puzzle-solving. It's about **resource management under temporal pressure** and **strategic decision-making with incomplete information**.

**Spatial Difficulty** (how much the player must monitor):
- **Easy (Era 1)**: One film, small studio (6 rooms). The player can see the entire studio at Studio Overview zoom. Monitoring is trivial.
- **Medium (Era 2-3)**: Two films, medium studio (10 rooms). The player must pan between rooms. Monitoring requires camera movement but is manageable.
- **Hard (Era 4-5)**: Three films, large studio (15+ rooms). The player cannot see everything at once. Monitoring requires strategic prioritization: "I check the Pipeline Board first, then respond to crises, then scan for yellows."

**Temporal Difficulty** (how much happens simultaneously):
- **Easy**: Long phase durations (3+ quarters per phase). The player has time to address decisions without rushing.
- **Medium**: Multiple films in different phases. Decisions overlap but are staggered. The player can address them sequentially.
- **Hard**: Multiple films in crisis simultaneously. Render farm overrun + animator quitting + budget overrun + rival release competing. The player must triage: "Which fire do I put out first?"

**Strategic Difficulty** (how opaque the systems are):
- **Easy**: Clear cause-and-effect. Decisions have visible, immediate feedback (e.g., "I approved crunch, morale dropped, I see the red icon above desks").
- **Medium**: Film DNA scores are estimations (+/- noise). The player understands causality but cannot min-max perfectly.
- **Hard**: Rival studios adapt to the player's strategy. Hidden risks in greenlight concepts. Long-term consequences (e.g., Studio Soul shifts) are not immediately visible.

### 7.2 Difficulty Curve Across Campaign

**Era 1 (Hours 1-2)**: Easy. One film, long phases, clear feedback. The player learns the systems without pressure.

**Era 2 (Hours 3-4)**: Medium. Two films, rival competition increases, Oscar pressure. The player is comfortable with individual systems and now learns to juggle.

**Era 3 (Hours 5-7)**: Hard. The 2D collapse crisis, budget pressure peaks, talent loyalty crises. This is the campaign's crucible. The player's mastery is tested.

**Era 4 (Hours 8-9)**: Medium-Hard. The player has adapted. Systems are mastered. Difficulty comes from optimization and legacy-building: "I could make a safe sequel, or I could risk everything on Jimmy's vision."

**Era 5 (Hours 10-12)**: Variable. The player can coast (make safe films, maintain profitability) or go for broke (pursue the perfect final film, risk bankruptcy for artistic legacy). Difficulty is player-driven.

### 7.3 Spatial Fail-States and Recovery

**Where does the player "die"?** They don't. FRAMEWAR has no hard fail-state (no game over screen). But it has **soft fail-states** that are spatially and emotionally painful:

**Bankruptcy Crisis**:
- Budget drops below -$30M.
- The player is summoned to the Executive Conference Room (a room they rarely visit).
- A lender's representative (NPC) appears, delivers the bad news: 30% staff layoffs, cancel one production, unfavorable distribution deal.
- The player chooses who to lay off (animator portraits appear, player clicks to dismiss).
- Empty desks appear across the studio.
- The spatial impact: walking through a half-empty studio is the punishment. The silence is the penalty.

**Talent Exodus**:
- If Studio Soul drifts too far toward EXECUTIVE and multiple high-VISION talents leave, the player's creative capacity craters.
- The spatial impact: empty desks, a storyboard room with no story artists, a Production Pipeline Board with no films because no Directors will work here.
- Recovery: Hire mid-tier talent, rebuild reputation through one safe commercial hit, slowly attract better talent back.

**Critical Failure Film**:
- A film bombs catastrophically (<$30M gross on a $100M budget, Projector Score below 40).
- The spatial impact: The film still appears on the filmography shelf, but it's visually marked (darker, smaller, a visible scar). Every time the player pans past the shelf, they see it.
- Recovery: The next film must succeed to restore confidence. The shadow of the flop lingers.

**The "Empty Shelf" Late Game**:
- If the player over-commits to productions and goes bankrupt before releasing many films, the endgame filmography shelf is sparse (2-3 films instead of 8-10).
- The spatial impact: The final retrospective pans across a mostly-empty shelf. The narration is muted. The legacy is thin.
- Recovery: None. This is the ending the player earned.

---

## 8. ENVIRONMENTAL STORYTELLING: THE STUDIO AS NARRATIVE

### 8.1 Passage of Time

The studio evolves visually across the 15-year campaign:

**Lighting** (changes based on era and time of day):
- Early game (1995-1998): Warm, optimistic lighting. Golden hour sunlight through windows in the afternoon.
- Mid-game (2003-2005): Harsher lighting during crises. Overcast skies visible through windows. The render farm's cool glow feels more oppressive.
- Late game (2006-2010): Mature, balanced lighting. Night scenes are more common (the studio runs late, lights on past midnight).

**Decor** (accumulates over time):
- Concept art on walls updates to reflect recent films.
- Awards (Oscars) appear in a glass case in the Lobby as they're won.
- Personal items on animator desks (photos, figurines, plants) increase as employees gain tenure.
- Empty desks after layoffs remain visually distinct (cleared surfaces, chairs pushed in, a ghostly absence).

**Technology** (visible upgrades):
- Render farm grows physically (more server racks added as tech tree advances).
- Monitors in the animation floor show higher-fidelity footage as ANIMATION QUALITY tech improves.
- The storyboard room's boards become more dense with panels as the player's productions become more complex.

**Seasonal/Temporal Cues**:
- The window in the Greenlight Office shows seasonal changes (palm trees in different light, rain during winter quarters, clear skies in summer).
- The calendar on the wall advances (pages flip with each quarter).
- The cityscape outside grows denser and more lit over 15 years (LA in 1995 vs. 2010).

### 8.2 Studio Soul Made Spatial

The player's Studio Soul (ARTIST vs. EXECUTIVE axis) manifests spatially:

**ARTIST-Leaning Studio** (Soul > +30):
- Storyboard room is messier: more concept art, more personal drawings pinned to walls, sketches on whiteboards.
- Animator desks are cluttered: reference books, action figures, coffee mugs, personal art.
- Lighting is warmer overall.
- The filmography shelf has more Oscar statuettes, fewer sequels.

**EXECUTIVE-Leaning Studio** (Soul < -30):
- Storyboard room is cleaner: marketing materials instead of concept art, production schedules instead of sketches.
- Animator desks are more uniform: fewer personal items, more corporate efficiency.
- Lighting is cooler, more fluorescent.
- The filmography shelf has more sequels, higher gross totals, fewer awards.

**Balanced Studio** (Soul -20 to +20):
- A mix of both aesthetics. Organized but human. Efficient but warm.

The player never sees a "Studio Soul: +45" number. They see the studio around them change. This is narrative through environment.

### 8.3 The Filmography Shelf as Endgame Narrative

The final shot of the game is a slow pan across the filmography shelf. The narration (procedurally generated based on the player's filmography) reflects on the studio's legacy. The shelf tells the story:

**The Prestige Studio**: A shelf full of Oscar winners, high Projector Scores, modest grosses. Narration: *"They didn't make the most profitable films. They made the ones people remember."*

**The Commercial Powerhouse**: A shelf full of sequels, massive grosses, few awards. Narration: *"They built an empire. They kept the lights on. They gave people what they wanted. Was that enough?"*

**The Innovator**: A shelf with high-ORIGINALITY films, a mix of hits and misses, a 2D film from 2005 that shocked the industry. Narration: *"They took risks. Some paid off. Some didn't. But no one can say they played it safe."*

**The Tragedy**: A sparse shelf (2-3 films, bankrupted mid-campaign). Narration: *"They burned bright and burned out. What they made was extraordinary. There just wasn't enough of it."*

The shelf is the score. The shelf is the ending. The shelf is the player's autobiography, written in film boxes and statuettes.

---

## 9. PLAYTESTING METRICS AND ITERATION PRIORITIES

### 9.1 What to Measure

**Spatial Comprehension**:
- Time-to-decision: How long does it take a player to find the room where a decision is needed after a notification pings?
- Target: <5 seconds by Hour 2 (player has learned the layout).
- If >10 seconds, the notification system or room layout needs adjustment.

**Navigation Efficiency**:
- Camera panning frequency: How many times does the player manually pan per quarter?
- Target: 3-5 pans per quarter in mid-game (efficient, purposeful movement).
- If >10 pans, the room jump system isn't being used (needs better tutorialization or more obvious room icons).

**Decision Pacing**:
- Pause duration: How long does the player pause when making a greenlight decision, director deviation approval, or crisis response?
- Target: 10-30 seconds for greenlight (considered but not paralyzed), 5-15 seconds for mid-production decisions (quick but meaningful), 30-60 seconds for crises (agonized).
- If <5 seconds for greenlight, decisions feel arbitrary (need more context/flavor). If >2 minutes, decision paralysis (too much information or unclear tradeoffs).

**Emotional Beats**:
- Post-release behavior: What does the player do immediately after a film releases?
- Target: 80%+ of players pan to the filmography shelf to see the new film (this indicates emotional investment in legacy).
- If <50%, the shelf isn't visually compelling or the release moment lacks impact.

**Spatial Learning Curve**:
- Time-to-find-room (first occurrence): When a new room is introduced (e.g., Post-Production Suite), how long does it take the player to find it when first needed?
- Target: <10 seconds (room should be adjacent to a known room, or notification system should guide).
- If >30 seconds, the room's spatial relationship to the pipeline is unclear.

### 9.2 Iteration Priorities

**Priority 1: The Production Pipeline Board** (Storyboard Room, west wall)
- This is the game's strategic map. If this isn't readable at a glance, the entire game fails.
- Playtest goal: Player can look at the Pipeline Board and verbally describe the state of all active films in <5 seconds.
- If not, iterate: card size, color coding, iconography, spatial arrangement.

**Priority 2: The Greenlight-to-Shelf Flow** (Tutorial path)
- The first film's journey from corkboard to filmography shelf is the tutorial. It must be seamless.
- Playtest goal: First-time player completes first film in <60 minutes, understands the spatial flow.
- If not, iterate: camera guidance, notification clarity, decision simplification.

**Priority 3: Crisis Moment Impact** (Animator quitting, bankruptcy, Ruth's departure)
- Crises must feel spatially and emotionally significant.
- Playtest goal: Player verbalizes emotional reaction (frustration, sadness, "oh no") during crisis events.
- If not, iterate: animation pacing, camera framing, silence/sound design, NPC staging.

**Priority 4: Multi-Film Juggling** (Mid-game, Era 2-3)
- Managing 2-3 films simultaneously is the game's cognitive peak. It must feel challenging but not overwhelming.
- Playtest goal: Player can triage 3 simultaneous decisions (one per film) in <2 minutes without visible stress.
- If not, iterate: auto-pause frequency, notification prioritization, advisor suggestions.

**Priority 5: The Filmography Shelf Moment** (Endgame retrospective)
- The final pan across the shelf must land emotionally.
- Playtest goal: Player sits in silence watching the retrospective (doesn't skip, doesn't alt-tab).
- If not, iterate: pacing of pan, narration quality, visual presentation of films on shelf.

---

## 10. LEVEL DESIGN CHECKLIST: DOES FRAMEWAR PASS THE GRID TEST?

Where does the player LOOK?
- At their work (storyboards, monitors, Pipeline Board, shelf). YES.
- At their people (animators at desks, directors in rooms, NPCs appearing for conversations). YES.
- At the results of their decisions (films on shelf, empty desks, render progress). YES.

What's the pacing here?
- Quarters are the heartbeat (2-3 minutes each, accelerated when desired). GOOD.
- Phases create rhythm (development → production → release, each with distinct tempo). GOOD.
- Crises punctuate (auto-pause, force attention). GOOD.
- Endgame slows for reflection (shelf retrospective). GOOD.

Every room teaches something. What does each room teach?
- Lobby: Your legacy is visible. The shelf is the goal. TEACHES.
- Greenlight Office: Films start here. Choices have weight. TEACHES.
- Storyboard Room: The Pipeline Board is your map. Time is spatial. TEACHES.
- Animation Floor: People make the work. Their morale matters. TEACHES.
- Render Farm: Technology is infrastructure. Over-allocation has consequences. TEACHES.
- Screening Room: Results are dramatic. You watch, you don't control. TEACHES.

What's the sightline?
- From Lobby, you see Greenlight Office (start here). CLEAR.
- From Greenlight Office, you see Storyboard Room (greenlighting sends films there). CLEAR.
- From Storyboard Room, you see Animation Floors and Render Farm (production happens there). CLEAR.
- From Animation Floor, you see Render Farm (the systems are connected). CLEAR.

Where's the breadcrumb?
- Notification pings (color-coded, spatial). PRESENT.
- Lit doorways (glowing when decisions are adjacent). PRESENT.
- Pulsing objects (Pipeline Board cards, corkboard concepts). PRESENT.
- Character placement (NPCs appear where decisions occur). PRESENT.

Does the player feel clever, not herded?
- The Pipeline Board teaches the flow, but the player chooses which films to prioritize. YES.
- Notifications guide attention, but the player decides when to address them. YES.
- Crises create pressure, but recovery paths are player-driven. YES.

Does the player feel like they work here?
- The studio accumulates personal history (empty desks, awards, concept art). YES.
- The player develops spatial memory ("I know where everything is"). YES.
- The player has routines (check Pipeline Board, scan for notifications, pan to shelf after release). YES.

Will the player remember this space long after they stop playing?
- The storyboard room's corkboards, covered in drawings. MEMORABLE.
- The render farm at night, monitors flickering. MEMORABLE.
- The filmography shelf, slowly filling. MEMORABLE.
- Dani's empty desk after she leaves. MEMORABLE.

**FRAMEWAR passes the GRID test.**

---

## FINAL STATEMENT

I've designed 50 levels for games that shipped. I've designed 100 levels for games that didn't. The levels that mattered -- the ones people remember -- are the ones where space told the story.

FRAMEWAR is one room: the studio. But within that room is an entire career. The player walks the same hallways for ten hours, and by the end, those hallways are home. They know which desk was Dani's. They know the corner of the storyboard room where the tough decisions happened. They know the way the render farm hums at 2 AM.

The studio is the level. The pipeline is the path. The shelf is the ending. Every film is a journey across the floor. Every decision is a room. Every crisis is a moment where the camera frames something you can't unsee.

Where does the player LOOK? At the work.
What's the pacing? The heartbeat of quarters, the breath of phases, the slow march toward legacy.
What does this space teach? That making something beautiful inside a system that rewards profit is a spatial problem. You stand in one room and decide. You walk to another and see the consequence. You return to the shelf and reckon with what you built.

That's the level design. That's the game.

Now build it. Then watch someone play it. If they walk through that studio at the end of the campaign and feel like they lived there, we did our job.

-- GRID

---

**File**: `/Users/burcukose/git/project-draft/games/12-framewar/level-design.md`
**Status**: Complete
**Next**: Art direction (PIXEL), Sound design (ECHO), Technical architecture (BYTE)
