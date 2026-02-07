# FRAMEWAR — Art Direction Document

**Art Director**: PIXEL
**Version**: 1.0
**Date**: 2026-02-07
**Status**: Production-Ready

---

## 1. VISUAL IDENTITY STATEMENT

### The Core Promise

FRAMEWAR is a game about making animated films. The visual identity must answer one question: **Does this look like a place where art is made?**

Not a sterile office. Not a factory floor. A creative studio at 2 AM where the render farm hums, coffee goes cold on desks, and storyboards cover every wall. The visual language is **tactile, warm, and human**. Every UI element exists in physical space. Every number lives on a surface. The player doesn't navigate menus — they walk through a studio that feels lived-in, aspired-to, and real.

### The Aesthetic Trinity

**1. Diegetic Physicality**
No floating menus. No abstract overlays. The production pipeline is a wall-mounted board with magnetic cards. The budget tracker is an LED ticker in the office. The filmography is a glass shelf with physical box art. Information lives in the world. The reference is not "UI design" — it's "production design."

Think: The Tacoma Gone Home school of environmental storytelling meets the corkboard aesthetic of True Detective's investigation wall. Every system is an object you can point a camera at.

**2. Studio Warmth**
This is not a cold, clinical workspace. Animation studios are creative sanctuaries — warm lighting, scattered concept art, personal touches. The color palette leans into deep browns, warm creams, amber lamplight. The render farm glows teal-blue in the dark. The screening room has that particular darkness of a theater mid-screening.

Think: The opening of Ratatouille when we see Gusteau's kitchen. The Pixar documentary "The Pixar Story" showing real studio spaces. The cozy chaos of a creative workspace in Into the Spider-Verse's art direction.

**3. Era-Authentic Texture**
The game spans 1995-2010. The visual language should subtly reflect this — CRT monitors in the early era transitioning to flatscreens, the physical media on the shelf (VHS boxes in 1998, DVD cases in 2003, Blu-ray in 2008), the aesthetic of pinned concept art and printed storyboards before everything went digital.

Think: The production design evolution across Mad Men seasons. The period-specific tech in Halt and Catch Fire. Details that players won't consciously notice but will subconsciously anchor the era.

### Visual Pillars (Non-Negotiable)

1. **Readability Over Beauty**: If a production board looks gorgeous but the player can't parse film status in 2 seconds, it's failed. Every visual must communicate first, decorate second.

2. **Tactile Interfaces**: Buttons feel like physical switches. Cards have paper texture. The storyboard room has thumbtack shadows. UI is not skin-deep — it has depth, material properties, and physicality.

3. **Four-Color Reputation System**: Gold (Prestige), Green (Commercial), Blue (Innovation), Purple (Artistic Courage). These colors are the visual spine of the game. They appear as accent lighting, as colored pins on corkboards, as LED indicators on the reputation display. The player should be able to glance at any screen and know which reputation axis is being referenced.

4. **The Studio as Stage**: The camera never leaves the studio. The entire game is set in this evolving space. As the studio grows (new wings, expanded render farm, bigger screening room), the player feels it spatially. The studio is both UI and character.

5. **No Character Faces**: Directors, animators, voice actors — all are represented by illustrated portraits in a consistent style (see Section 6). We never render 3D character models. This keeps scope manageable and maintains the game's meta-commentary on animation production without becoming an animation itself.

### Visual Reference Constellation

When describing FRAMEWAR's look to an artist:

**"It's the corkboard and pushpin aesthetic of Cultist Simulator, the warm isometric studio spaces of Unpacking, the diegetic UI philosophy of Obra Dinn and Tacoma, the period texture of Mad Men's production design, and the emotional warmth of a Pixar 'making of' documentary. It feels like walking into an animation studio at midnight and feeling both the pressure and the magic."**

That paragraph is the art direction in 60 words. Everything downstream serves that image.

---

## 2. COLOR PALETTE

### Primary Palette (Studio Environment)

**Studio Deep Brown** — `#2C1810`
Usage: Primary background for studio walls, shadows, dark surfaces. This is the color of a creative space at night. It holds the warm tones without overwhelming them. Use for: base walls, shadowed areas, furniture silhouettes.

**Warm Cream** — `#F5E6D0`
Usage: Primary light source reflections, illuminated walls, paper surfaces. This is lamplight hitting a wall. Use for: lit wall sections, desk surfaces, the general "warmth" glow of the studio at night.

**Storyboard Paper** — `#FFF8E7`
Usage: All storyboard cards, concept art sheets, documents pinned to boards. Slightly warmer than pure white. Feels like quality drawing paper under tungsten light. Use for: every piece of pinned paper, every document the player clicks.

**Charcoal Gray** — `#3D3D3D`
Usage: Text on light backgrounds, metal surfaces, inactive UI elements. Use for: body text, metal desk legs, unpowered monitors, steel render farm chassis.

**Soft Black** — `#1A1A1A`
Usage: Deep shadows, active text on light backgrounds, separator lines. Never pure black — always slightly warm. Use for: text, shadows under objects, window frames at night.

### Reputation Accent Colors (The Four-Color System)

**Prestige Gold** — `#C4A84D`
RGB: 196, 168, 77
Usage: Awards, Oscar statues, premium talent indicators, critical acclaim highlights, films with Projector Score 80+. Appears as warm brass/gold metal, as accent lighting in the awards shelf area, as colored pins marking prestigious projects.

Visual rule: Gold never appears in large fields. Always accents, highlights, metallic surfaces, point lights.

**Commercial Green** — `#2ECC71`
RGB: 46, 204, 113
Usage: Box office numbers, revenue indicators, profitable project markers, market success signals. A fresh, modern green that feels like "money in the bank."

Visual rule: Green appears on LED displays, digital readouts, the box office ticker. It's the color of numbers that make the studio happy.

**Innovation Blue** — `#3498DB`
RGB: 52, 152, 219
Usage: Technology, render farm indicators, tech tree nodes, CG production markers, technical breakthroughs. A cool, electric blue that feels like screens and processing.

Visual rule: Blue is the color of machines. Render farm monitors glow blue. Tech tree nodes are blue circuits. CG films have blue accent pins.

**Artistic Courage Purple** — `#9B59B6`
RGB: 155, 89, 182
Usage: High-originality projects, 2D animation markers, director's vision indicators, artistic risk highlights. A deep, confident purple that feels both royal and rebellious.

Visual rule: Purple appears as accent lighting around the 2D animation wing, as pins marking artistic projects, as the glow around films with ORIGINALITY 8+.

### Secondary Accent Colors

**Crisis Red** — `#E74C3C`
RGB: 231, 76, 60
Usage: Budget overruns, production problems, morale warnings, box office disasters. Use sparingly — red is alarm state.

Visual rule: Red only appears when something is wrong. A red pin on a production card means a crisis. A red LED on the budget tracker means trouble.

**Render Farm Teal** — `#1ABC9C`
RGB: 26, 188, 156
Usage: Active render farm glow, processing indicators, "working late" atmosphere. A softer, more ambient blue-green than Innovation Blue.

Visual rule: Teal is ambient. It's the light that spills from monitors when the studio is dark. It's the color of machines doing their job.

**Warning Amber** — `#F39C12`
RGB: 243, 156, 18
Usage: Caution states, scheduling conflicts, morale at-risk, tech tree research in progress. Not quite alarm red, but "pay attention."

Visual rule: Amber appears on status indicators that need the player's attention but aren't critical yet.

### Palette Usage Rules

**Rule 1: Warm Base, Cool Accents**
The studio environment is warm (browns, creams). The interactive systems are cool (blues, teals) or saturated (gold, green, purple, red). This creates clear visual hierarchy: the world is warm, the data is cool.

**Rule 2: Never Use Pure White or Pure Black**
Pure white (`#FFFFFF`) is harsh and breaks the warm atmosphere. Use Storyboard Paper or Warm Cream instead. Pure black (`#000000`) is too deep. Use Soft Black with a hint of warmth.

**Rule 3: Reputation Colors Never Mix**
Gold, green, blue, and purple are the game's color-coded reputation system. They never blend, never overlap, never appear in gradients together. A film can have multiple reputation impacts, but the visual presentation keeps them separated (e.g., a gold pin AND a green checkmark, not a gold-green hybrid).

**Rule 4: Saturation Budget**
Only reputation colors and warning states get high saturation. The environment is desaturated. This keeps the player's eye on the information that matters. A room full of saturated colors is visual noise. A warm neutral room with strategic pops of gold/green/blue/purple is readable interface design.

**Rule 5: Light Sources Are Diagetic**
Every light has a source. The desk lamp casts Warm Cream light. The render farm monitors emit Render Farm Teal. The LED ticker glows Commercial Green. We never use ambient lighting that doesn't have a visible source object.

### Color Accessibility

**Colorblind Considerations**:
The four reputation colors must be distinguishable by players with deuteranopia and protanopia (red-green colorblindness).

Test: Gold `#C4A84D` and Green `#2ECC71` have sufficient luminance contrast (gold is darker, green is brighter). Blue `#3498DB` and Purple `#9B59B6` are separable by hue shift.

Backup: Every reputation color also has a shape/icon pairing:
- Prestige Gold = Trophy icon
- Commercial Green = Dollar sign icon
- Innovation Blue = Gear icon
- Artistic Courage Purple = Palette icon

Even in grayscale, the player can distinguish systems by icon shape.

---

## 3. SHAPE LANGUAGE GUIDE

### Primary Shapes

The game's visual grammar is built on three shape families:

**Rectangles and Cards (Information)**
All film concepts, production cards, talent profiles, and storyboard frames are rectangular. Rectangles mean "discrete information unit." The player learns: rectangle = something I can evaluate and decide on.

Proportions:
- Film concept cards: 3:4 aspect ratio (portrait), sized to feel like an index card
- Production pipeline cards: 16:9 aspect ratio (landscape), sized to show at-a-glance status
- Storyboard frames: 2.39:1 aspect ratio (cinemascope), mimicking film aspect ratios

Corners: Slightly rounded (2-4px radius). Never sharp 90-degree corners. Paper has softness.

**Circles and Dots (Status and Progress)**
All progress indicators, status LEDs, and notification badges are circular. Circles mean "state" or "process ongoing."

Usage:
- Render farm progress indicators: filled circle = rendering, hollow circle = queued
- Talent morale: colored dot (green/yellow/red) next to portrait
- Film phase completion: circles that fill as quarters progress

**Horizontal Lines (Structure and Flow)**
The production pipeline, the timeline, the budget tracker — all horizontal. Horizontal lines mean "progression through time."

The production pipeline is the game's visual anchor: a horizontal board divided into six sections (DEV, PRE, PROD, POST, MKT, REL) with film cards moving left to right. This is the spine. Every player will learn to read left = early, right = release.

### Secondary Shapes

**Pins and Thumbtacks (Attachment and Importance)**
Every storyboard, every concept, every note is "pinned" to a surface. The pin/thumbtack is the visual metaphor for "this matters enough to be placed."

Rendering: Pins cast small shadows. They have colored tops (matching reputation colors when relevant). When a card is "unpinned" (a film is canceled, a concept is rejected), the pin is removed and the card fades.

**Corkboard Texture (Background for Information)**
Corkboard is the substrate for all paper-based information. It provides texture and warmth. The grain is subtle — visible at normal viewing distance but not distracting.

Usage: The greenlight table background is cork. The storyboard room walls are cork. The production pipeline board backing is cork. Cork means "creative workspace."

**Glass and Reflection (Achievement and Display)**
The filmography shelf is glass and metal. Released films are displayed behind glass like museum pieces. Glass surfaces are the only place we use specular highlights and reflections. Glass means "finished, permanent, legacy."

### Shape Composition Rules

**Rule 1: Alignment Grid**
All UI elements snap to an 8px grid. Cards, buttons, text — everything aligns. Pixel-perfect alignment communicates care and professionalism. A sloppy grid communicates a sloppy studio.

**Rule 2: Asymmetric Balance**
The studio spaces are not symmetrical. The render farm is off to one side. The storyboard room is larger than the screening room. Asymmetry feels organic and lived-in. Perfect symmetry feels corporate and sterile.

But: within a single UI element (a film card, a button, a status panel), symmetry and alignment are preserved. The composition can be asymmetric, but the components are structured.

**Rule 3: Layering Depth**
Cards sit ON surfaces. Surfaces sit IN rooms. Rooms exist IN the studio. The visual depth hierarchy is always clear:
1. Background room (walls, floors)
2. Furniture and fixtures (desks, boards, shelves)
3. Cards and documents (film concepts, storyboards)
4. Active overlays (tooltips, decision prompts)

Each layer has subtle shadow and elevation cues. A card hovers 2-4px above its surface with a soft shadow.

**Rule 4: No Floating Elements**
Everything is attached to something. A film card is pinned to a board. A status indicator is mounted on a wall. A tooltip appears as a post-it note stuck to a surface. We never use abstract HUD elements floating in undefined space.

Exception: The pause menu. When the player pauses, the studio dims and a centered menu appears. This is acceptable because pause is a meta-game state, not a diegetic action.

### Icon Design Principles

Icons are **flat, two-color, and immediately parseable**.

Style reference: Not pixel art, not photorealistic, not skeuomorphic. Think: simplified pictograms with personality. Similar to: Monument Valley's icon language, Mini Metro's symbol set, or Apple SF Symbols but warmer.

Palette: Icons use Charcoal Gray `#3D3D3D` on light backgrounds, Warm Cream `#F5E6D0` on dark backgrounds. Accent colors (gold/green/blue/purple) are used sparingly for status states.

Size: Icons are minimum 24x24px at base resolution. Any smaller and readability breaks.

Examples:
- Director icon: Simplified director's chair or megaphone
- Animator icon: Pencil and paper
- Voice Actor icon: Microphone
- Render Farm icon: Server rack or processing symbol
- Awards icon: Trophy or star
- Budget icon: Dollar sign or coin
- Calendar/Schedule icon: Calendar page

Each icon is designed at 64x64px and scaled down. This ensures clarity at small sizes.

---

## 4. STYLE RULES (DO'S AND DON'TS)

### Typography

**DO:**
- Use a single font family with multiple weights for hierarchy
- Recommended: A geometric sans-serif with warmth (think: Outfit, Plus Jakarta Sans, or Inter with adjusted letter-spacing)
- Establish clear type scale: Body (14-16px), Subhead (18-20px), Heading (24-28px), Display (36-48px for film titles)
- Use medium-to-heavy weights (500-600) for UI labels to ensure readability on varied backgrounds
- Maintain minimum 1.4em line-height for body text
- Left-align text blocks. Center-align only for titles or single-line emphasis

**DON'T:**
- Don't use more than one typeface (exception: handwritten notes can use a script font for flavor, but sparingly)
- Don't set body text below 14px. Ever. Tiny text kills readability
- Don't use pure white text on pure black backgrounds (use Warm Cream on Soft Black)
- Don't use decorative or script fonts for functional UI. Script fonts can appear on in-world documents (director's notes) but never on buttons or labels
- Don't use all-caps for blocks of text. All-caps is acceptable for short labels (MAX 3-4 WORDS) but becomes unreadable in paragraphs

**Special Case: Film Titles**
Film titles appearing on posters/boxes in the filmography shelf can use custom display type per film. This adds personality and reflects the in-universe branding of each film. But the game's UI text stays consistent.

### Animation and Motion

**DO:**
- Use easing functions (ease-in-out, cubic-bezier). No linear motion except for mechanical processes (render progress bars)
- Short durations: 150-250ms for UI responses (button hovers, card flips), 300-500ms for state transitions (panel slides, screen changes)
- Animate on purpose: motion should communicate change of state or direct attention. Random animation is noise
- Use subtle parallax when camera moves through the studio (background moves slower than foreground)
- Animate numbers counting up (box office revenue rolling in) for dramatic effect

**DON'T:**
- Don't use animation durations over 800ms for functional UI. Players will spam-click to skip. Reserve long animations (1-2 seconds) for cinematic moments (Oscar announcement)
- Don't animate everything. A button that bounces on hover is cute the first time and annoying the 50th time. Favor subtle state changes (color shift, slight scale) over complex motion
- Don't use animation to hide loading. If something takes 2 seconds to load, show progress. Don't use a 2-second animation as fake loading
- Don't auto-play looping animations everywhere. The render farm can have subtle pulsing lights. But if every object is animating, the screen becomes visual chaos

**Key Animation Moments** (these should feel special):
1. Greenlighting a film: The concept card gets stamped with a "GREENLIT" approval, then slides onto the production pipeline board
2. Film release: The box office ticker counts up over 2-3 seconds as opening weekend numbers roll in
3. Award win: The trophy icon fades in with a golden glow and a subtle chime
4. Studio expansion: Camera pulls back to reveal the new wing, then settles into the new default view

### Lighting and Atmosphere

**DO:**
- Use warm practical light sources (desk lamps, overhead tungsten lights) as primary lighting
- Create zones of light and shadow. The screening room is darker than the storyboard room
- Show time-of-day through window light (if visible): blue dawn light at 6 AM, warm sunset at 6 PM, dark with city lights at night
- Use rim lighting to separate objects from backgrounds (a subtle bright edge on the left or top of cards)
- Make the render farm glow increase when processing is active (more teal ambient light at night when renders are running)

**DON'T:**
- Don't use flat, even lighting. That's corporate office aesthetics. We're making art here
- Don't make the studio too dark. Atmospheric is good. Eye strain is bad. Maintain readability first
- Don't use colored lighting everywhere. The four reputation colors appear as accent lights in specific locations (the awards shelf glows gold). Overuse kills the effect
- Don't change lighting dramatically during gameplay. Time-of-day can subtly shift, but the player shouldn't feel like the room is pulsing. Consistency aids readability

**Atmospheric Details** (visual flavor, not functional):
- Dust motes in light beams from windows
- Steam rising from coffee cups on desks
- Subtle film grain texture overlay (10-15% opacity max, barely visible, adds warmth)
- Glow/bloom on monitor screens and LED displays (subtle, not overdone)

### Texture and Material

**DO:**
- Use subtle paper grain on all document surfaces (storyboards, concept cards)
- Add slight fabric weave to corkboard backgrounds
- Show brushed metal texture on render farm chassis and film shelf
- Render wood grain on desks (subtle, not photorealistic)
- Use matte materials as default. Gloss/reflection only on glass and screens

**DON'T:**
- Don't make textures high-contrast. They should add tactile quality without dominating. If the player notices the texture before the information, it's too strong
- Don't use photographic textures. Stylized, illustrated textures only
- Don't mix texture styles. If corkboard is illustrated, everything is illustrated. No mixing illustrated backgrounds with photorealistic objects
- Don't apply textures to interactive elements like buttons. Buttons should be flat colors with subtle gradients at most

**Material Palette**:
- Paper: Warm cream with subtle grain
- Cork: Medium brown with organic dot pattern
- Wood: Deep brown with linear grain
- Metal: Cool gray with brushed horizontal lines
- Glass: Transparent with subtle specular highlights
- Fabric (if used on chairs): Matte solid colors, no patterns

### UI Component Style

**Buttons**
DO:
- Clear hover state (slight brightness increase, 110% scale, or subtle shadow)
- Rounded corners (4-6px radius)
- Adequate padding (12px vertical, 20px horizontal minimum)
- High contrast text (Soft Black on Warm Cream, or Warm Cream on a saturated accent color)

DON'T:
- No gradient fills (flat or single subtle gradient max)
- No drop shadows on buttons (reserve shadows for elevated cards)
- No overly decorative button shapes (circles, stars, etc.). Rectangles communicate "clickable"

**Input Fields**
DO:
- Inset appearance (subtle inner shadow)
- Clear focus state (border color change to Innovation Blue)
- Placeholder text at 60% opacity

DON'T:
- No borderless inputs. Always have a defined edge
- No tiny input fields. Minimum 36px height for touch-friendly design (even though PC is primary platform, ergonomics matter)

**Cards (Film Concepts, Talent Profiles, etc.)**
DO:
- Consistent card sizes within a category (all film concepts are the same size)
- Elevation shadow (2-4px offset, 20-30% opacity, soft edge)
- Hover state: slight raise (increase shadow, slight scale)
- Pin graphic at top (colored thumbtack matching reputation if applicable)

DON'T:
- No cards without shadows (shadow = elevation = interactivity)
- No cards with borders AND shadows (choose one separation method)
- No tilted/rotated cards in grid views (can be used sparingly for decorative pinned notes, never for functional elements)

**Progress Bars**
DO:
- Clear unfilled background (light gray or warm cream)
- Filled portion uses context color (blue for rendering, green for budget filling, amber for warning states)
- Numeric percentage if space allows
- Rounded ends (pill shape)

DON'T:
- No striped/animated fills (unless indicating active processing, then subtle diagonal stripes)
- No overly thick progress bars (6-10px height is sufficient)

---

## 5. ASSET PIPELINE OVERVIEW

### Production Workflow

**Stage 1: Concept and Approval**
Art Director (that's me) creates style guide and reference boards. Team reviews. Iterate until the vibe is locked.

**Stage 2: Asset Creation**
All assets created in vector (Adobe Illustrator or Figma) for UI elements, or 2D illustration software (Procreate, Photoshop) for environmental art.

Target resolution: 1920x1080 base canvas. All assets designed at 2x resolution (3840x2160) and scaled down for crisp rendering. This allows 4K support without re-asset.

**Stage 3: Implementation**
Assets exported as PNG (for illustrations, environmental art) or SVG (for icons, UI components).

Engine: Assuming Unity or Godot. Assets imported, placed in scene.

**Stage 4: Lighting and Post-Processing**
In-engine lighting setup: warm ambient light, practical light sources (lamps, monitors), subtle post-processing (film grain, slight vignette, color grading to push warmth).

**Stage 5: UI Functionality Build**
Engineers hook up interactivity. Art Director reviews to ensure hover states, animations, and transitions match vision.

**Stage 6: Iteration and Polish**
Playtest for readability. Adjust colors, sizes, layouts based on feedback. Iterate until the player can parse the screen in 2 seconds.

### File Organization

```
/Assets
  /UI
    /Buttons
    /Cards
    /Icons
    /Panels
  /Studio
    /Greenlight_Room
    /Storyboard_Room
    /Render_Farm
    /Screening_Room
    /Filmography_Shelf
  /Portraits
    /Directors
    /Animators
    /VoiceActors
  /Effects
    /Particles (dust motes, steam)
    /Lighting (glow maps, light shafts)
  /Textures
    /Paper
    /Cork
    /Wood
    /Metal
```

Naming convention: `CategoryName_Descriptor_State.png`
Example: `Button_Greenlight_Hover.png`, `Card_FilmConcept_Default.png`

### Technical Constraints

**Resolution Support**:
- Base: 1920x1080
- Minimum: 1366x768 (UI must remain readable, may require dynamic scaling)
- Maximum: 4K (3840x2160) (assets are 2x resolution, so native support)

**Aspect Ratios**:
- Primary: 16:9
- Secondary: 16:10 (small letterboxing acceptable)
- Ultrawide: Not prioritized for v1, but UI should be anchored to avoid stretching

**Performance Budget**:
- Studio scene must run at 60fps on mid-tier hardware (GTX 1060 equivalent)
- Max simultaneous animated elements: 20-30 (render farm monitors, progress bars, ambient particles)
- Draw call budget: Keep UI atlased to minimize draw calls (target <100 per frame for UI layer)

**Texture Memory**:
- UI atlas: 2048x2048 max
- Environmental art: Individual assets max 1024x1024
- Portraits: 512x512 per character

### Animation Technical Specs

**Frame Rate**:
- UI animations: 60fps
- Ambient effects (dust motes, steam): 30fps is acceptable

**Timing Reference**:
Button hover: 150ms ease-in-out
Panel slide in/out: 300ms ease-out
Card flip: 400ms cubic-bezier
Number count-up: 2000ms ease-out (for dramatic box office reveals)

**Easing Functions**:
Default: `cubic-bezier(0.4, 0.0, 0.2, 1)` (material design standard ease)
Bouncy (for greenlight stamp): `cubic-bezier(0.68, -0.55, 0.265, 1.55)`
Smooth stop: `ease-out`

### Localization Considerations

**Text Expansion**:
UI must accommodate 30-40% text expansion for languages like German or French.

Design solution: Buttons and labels have flexible width (horizontal padding can expand). Cards have fixed dimensions, so text must wrap or truncate with ellipsis.

**Font Support**:
Primary font must support Latin Extended, Cyrillic (if targeting Russian market), and ideally CJK (Chinese, Japanese, Korean) if targeting Asian markets.

Backup: If primary font doesn't support CJK, use system fallback fonts for those languages.

**Right-to-Left (RTL) Languages**:
Not prioritized for v1. If Arabic/Hebrew support is added later, the entire UI layout flips. The production pipeline board would read right-to-left, which is mechanically fine (still a progression).

---

## 6. CHARACTER PORTRAIT STYLE

Since Directors, Animators, Voice Actors, and Story Artists are key to the Talent Engine, they need visual representation. But we're not rendering 3D characters. Instead: illustrated portraits.

### Portrait Style Definition

**Medium**: Digital illustration, painterly but not photorealistic.

**Reference Point**: The character portraits in Hades (Supergiant Games) — expressive, stylized, vibrant, with strong silhouettes and personality. But warmer in tone. Less mythic, more human.

Alternate reference: The illustrated portrait style in Citizen Sleeper — softer, more intimate, slightly abstract.

### Technical Specs

**Dimensions**: 512x512px, exported at 1024x1024 for retina/4K support
**Aspect Ratio**: 1:1 (square)
**Framing**: Head and shoulders, centered. Facing forward or slight 3/4 turn. No extreme angles.

**Color Palette**: Portraits can use a slightly broader palette than the UI (skin tones, hair colors, clothing), but they should harmonize with the overall warm aesthetic. Avoid pure whites and pure blacks in portraits. Push toward warm shadows.

**Background**: Solid color or subtle gradient. Background color can hint at the character's role:
- Directors: Prestige Gold tint
- Animators: Innovation Blue tint
- Voice Actors: Commercial Green tint
- Story Artists: Artistic Courage Purple tint

The tint is subtle (10-15% saturation), not garish.

### Visual Diversity

The talent pool must be visually diverse:
- Range of ages (young animators fresh out of school, veteran directors)
- Range of ethnicities (animation is global)
- Range of gender presentations
- Range of personal styles (some wear suits, some wear hoodies, some have visible tattoos)

Diversity is not just ethical — it's mechanically correct. The animation industry in this era was diversifying. Homogenous portraits would be historically inaccurate.

### Expression and Personality

Each portrait conveys personality through:
- Expression (confident smirk, serious intensity, friendly warmth, exhausted burnout)
- Costume/styling (a buttoned-up director, a paint-splattered animator, a glamorous voice actor)
- Small details (glasses, a specific hairstyle, a visible sketchbook in frame)

The player should be able to look at a portrait and get a sense of who this person is before reading their stats. A high-EGO director looks different from a high-VISION/low-EGO director.

### Production Method

**Concept**: Define 20-30 "archetypes" (The Visionary Director, The Burnt-Out Veteran, The Rising Star, The Celebrity Voice Actor, The Perfectionist Animator, etc.)

**Illustration**: Hire 1-2 character illustrators. Provide archetype descriptions, reference mood boards, and technical specs. Illustrators produce 50+ portraits across archetypes with variations.

**Procedural Variants**: For extended play, portraits can be procedurally tinted or slightly modified (palette swap, accessory toggles) to create additional variants without full re-illustration. But the base library is authored art.

---

## 7. STUDIO ENVIRONMENT DESIGN

The studio is the game. Every system is a room or a wall. Here's the spatial breakdown.

### Overview Layout (Isometric View)

The default camera is isometric, angled ~30 degrees from top-down. Think: Unpacking, A Little to the Left, or Monument Valley's camera angles. The player can see into rooms, see the depth of the space, but still maintain readability of flat UI elements.

Camera movement: The player can pan the camera to different rooms, or click on room hotspots to jump to a focused view. No manual 3D camera control — pre-defined camera positions for each room.

### Room-by-Room Breakdown

#### 1. The Greenlight Office

**Function**: The Greenlight Table. Where film concepts are reviewed and greenlit.

**Visual Description**:
A corner office with large windows (city skyline visible at night). A desk with a warm desk lamp (Warm Cream light pool). The corkboard wall behind the desk is covered with pinned film concept cards. Each card is a 3:4 rectangle with a title, logline, and visible attribute icons (ORIGINALITY, AUDIENCE BREADTH, etc.).

Cards the player hasn't reviewed yet have a subtle pulsing glow (attention indicator). Greenlit cards are stamped and move to the production pipeline board.

On the desk: a coffee cup (steam rising), a pen, scattered notes. The Oscar statuette (if won) sits on the desk corner, catching gold light.

**Atmosphere**: This is the decision room. It should feel both aspirational (big windows, nice desk) and pressurized (the weight of decisions). Warm, but serious.

**Lighting**: Desk lamp primary, window backlight secondary. If it's night in-game, the city lights outside twinkle.

#### 2. The Production Pipeline Board

**Function**: The central strategic interface. Shows all active films and their phase status.

**Visual Description**:
A long wall-mounted board divided into six vertical sections: DEVELOPMENT, PRE-PRODUCTION, PRODUCTION, POST-PRODUCTION, MARKETING, RELEASE. Each section has a label and a colored accent stripe (subtle, not overpowering).

Film cards sit in their current phase, pinned with colored thumbtacks matching their reputation trajectory (gold for prestige projects, green for commercial, etc.). Each card shows:
- Film title
- Current phase progress (circular progress indicator)
- Budget status (green = on budget, amber = risk, red = overrun)
- Director portrait (small)

Clicking a card opens a detailed view of that film's current phase decisions.

**Atmosphere**: This is mission control. It should feel organized, legible, slightly industrial (metal frame holding the board). The spine of the operation.

**Lighting**: Overhead fluorescent lights (cool white), with accent lighting from below highlighting the board.

#### 3. The Storyboard Room

**Function**: Where the player reviews storyboards, makes Development and Pre-Production decisions.

**Visual Description**:
Walls covered in cork. Hundreds of storyboard frames pinned in rough grids (not perfectly aligned — artistic chaos). A large table in the center with more storyboards spread out. Warm overhead lights.

When the player clicks into a film's Development or Pre-Production phase, the camera focuses on a section of wall dedicated to that film. The storyboard panels are arranged in sequence. The player can click panels to zoom in and review.

**Atmosphere**: Creative, energetic, slightly messy. This is where story happens. Warmer lighting than the pipeline board. Feels lived-in.

**Lighting**: Multiple warm overhead lamps creating pools of light.

#### 4. The Render Farm

**Function**: Visual representation of production processing. Where the player sees CG films being rendered.

**Visual Description**:
A wall of rack-mounted servers and monitors. Each monitor shows a simplified view of what's rendering: progress bars, previsualization wireframes, status LEDs. The room glows teal-blue (Render Farm Teal) when renders are active.

Render progress for active films is visible here. Each film in the PRODUCTION phase has a dedicated monitor showing its render percentage.

The sound design here is crucial: a low hum of cooling fans, the occasional beep of a process completing.

**Atmosphere**: Technological, cool-toned (contrasting the warm storyboard room), slightly ominous. The machines never sleep. Feels like the engine room of a ship.

**Lighting**: Monitor glow (teal-blue), overhead industrial lights (cool white).

#### 5. The Screening Room

**Function**: Where the player reviews "dailies" (production quality checks) and watches box office results during release.

**Visual Description**:
A small theater. Rows of 3-4 plush seats facing a projection screen. The room is dark except for the glow of the screen and subtle aisle lighting.

When the player reviews dailies, the screen shows a simplified animatic (storyboard frames in sequence, not full animation). When a film is in release, the screen displays the box office tracker: a large LED-style display counting up revenue, showing week-over-week numbers.

**Atmosphere**: Intimate, quiet, focused. This is the moment of truth. Dark except for the screen. Feels like watching your child perform on stage.

**Lighting**: Screen glow (warm or cool depending on content), subtle aisle lights.

#### 6. The Filmography Shelf

**Function**: Displays the player's completed films. The legacy showcase.

**Visual Description**:
A glass and metal shelf in the studio lobby. Each released film is displayed as a box (VHS case in 1995, DVD case by 2003, Blu-ray by 2008). The box art is procedurally generated based on Film DNA (genre, tone, key visual elements).

Each box shows:
- Film title
- Box art
- Small icons indicating awards won (Oscar trophy, other accolades)
- Total gross (numeric display)

The shelf fills left-to-right as films release. By the end of the campaign, 8-10 films are on display. The player can click a box to view detailed stats (DNA scores, reviews, box office trajectory).

Awards won (Oscar statues, critic trophies) are displayed next to the corresponding film.

**Atmosphere**: Pride. Reflection. Legacy. This should feel like a museum exhibit. The glass catches reflections. The lighting is warm but reverent.

**Lighting**: Warm spotlights on the shelf from above, slight reflection on the glass.

#### 7. Talent Office / Roster

**Function**: Where the player reviews their staff, hires new talent, manages morale.

**Visual Description**:
A wall of portrait frames (the illustrated character portraits) arranged in a grid. Each portrait is labeled with name, role, and key stats. Morale is indicated by a colored dot (green = happy, yellow = stressed, red = at-risk).

Available-for-hire talent appears in a separate section (like a corkboard with resumes pinned).

**Atmosphere**: Human. This is the people side of the studio. Warmer than the render farm, more structured than the storyboard room.

**Lighting**: Warm overhead lights, similar to the greenlight office.

### Studio Expansion

As the player invests in studio upgrades (unlocking a 3rd production slot, upgrading the render farm), new rooms or expanded wings are added.

**Visual Indication**: Camera pulls back to reveal the new space. The layout shifts to accommodate. New rooms maintain the established aesthetic (warm lighting, cork/wood/metal materials) but each has a distinct function and atmosphere.

Example: Expanding the render farm adds a second wall of monitors. Expanding production capacity adds a second storyboard room.

---

## 8. READABILITY CHECKLIST

This is the operational test. A beautiful game that can't be parsed is a failed game.

### The Two-Second Test

**Test**: Show a screenshot of the Production Pipeline Board to a new player. In two seconds, can they identify:
1. How many films are in production?
2. Which film is furthest along?
3. Are any films in trouble (budget, schedule)?

**Pass Condition**: 80%+ of test players answer all three correctly.

**Design Solutions to Ensure Pass**:
- Film cards are color-coded by status (green border = healthy, amber border = at-risk, red border = crisis)
- Pipeline phases are clearly labeled with large text
- Position on the board = progression (left = early, right = late)

### The Squint Test

**Test**: Blur the screen (Gaussian blur, ~10px radius). Can the player still identify:
1. Major UI zones (which room is which)?
2. Interactive elements (where to click)?
3. Status at a glance (good vs. bad)?

**Pass Condition**: Major zones and status indicators are distinguishable even blurred.

**Design Solutions**:
- High contrast between zones (dark render farm vs. warm storyboard room)
- Size differentiation (larger elements are more important)
- Color coding (green = good, red = bad, even when blurred)

### The Colorblind Test

**Test**: Convert the UI to grayscale. Can the player still distinguish the four reputation systems?

**Pass Condition**: Yes, via icons and shape.

**Design Solutions**:
- Every reputation color has a paired icon (trophy, dollar, gear, palette)
- Even in grayscale, luminance differences separate gold (darker), green (brighter), blue (mid), purple (mid-dark)

### The Icon Recognition Test

**Test**: Show a player 10 icons without labels. Can they identify what each represents?

**Pass Condition**: 70%+ correct identification.

**Design Solutions**:
- Icons are literal, not abstract (microphone = voice actor, not a generic "person")
- Icons are tested with players before finalizing

### The Glance-to-Action Test

**Test**: Tell a player "greenlight the film with the highest originality score." Time how long it takes them to find and click it.

**Pass Condition**: <5 seconds.

**Design Solutions**:
- Film concept cards display ORIGINALITY as a prominent numeric value or bar
- Cards are sortable/filterable by attribute
- Hover states highlight the full card to confirm selection before click

### The Decision Context Test

**Test**: When a decision prompt appears ("Your director wants to extend Development by 1 quarter. Cost: +$3M. STORY DEPTH +0.5. Approve?"), does the player have enough context to decide without navigating away?

**Pass Condition**: 90%+ of players can make the decision based on the prompt alone.

**Design Solutions**:
- Decision prompts show relevant current stats (current budget, current STORY DEPTH score)
- Consequences are clearly labeled ("Budget: $80M → $77M")
- A "more info" tooltip is available but not required

### The Performance Readability Test

**Test**: At 60fps with all animations running (render farm monitors pulsing, progress bars filling, ambient particles), does the UI remain readable?

**Pass Condition**: Yes. No flickering, no competing motion that distracts from information.

**Design Solutions**:
- Ambient animations are slow and subtle (1-2 second cycles)
- No more than 3-4 animated elements in a single view
- Critical information (text, numbers) never animates unless it's a deliberate effect (counting up box office numbers)

---

## 9. REFERENCE LIST

This is the visual education. Every artist on the team should study these references to internalize the tone.

### Games (Visual and UI Design)

**Cultist Simulator** (Weather Factory, 2018)
Why: Tactile card-on-table interface, diegetic UI, the feeling of arranging physical objects.
Study: The way cards have weight and texture. The corkboard aesthetic. The sense of ritual in placing objects.

**Unpacking** (Witch Beam, 2021)
Why: Isometric domestic spaces, warm color palette, environmental storytelling through objects.
Study: The warmth of the lighting. The way objects feel placed, not floating. The sense of a lived-in space.

**Return of the Obra Dinn** (Lucas Pope, 2018)
Why: Diegetic UI (the book interface), period-appropriate aesthetics, information as physical object.
Study: How the book interface makes information feel tactile and grounded in the world.

**Hades** (Supergiant Games, 2020)
Why: Character portrait style — expressive, stylized, vibrant.
Study: The portraits. How much personality is conveyed in a single frame. The color saturation and warmth.

**Citizen Sleeper** (Jump Over The Age, 2022)
Why: UI design that's functional and beautiful. Clean typography, strong color coding, readability.
Study: The stat displays. The way information is organized. The sci-fi aesthetic that's warm, not cold.

**Monument Valley** (ustwo games, 2014)
Why: Isometric perspective, clean shape language, color as mood.
Study: The camera angles. The way simple shapes create complex spaces. The use of color to guide the eye.

**A Short Hike** (adamgryu, 2019)
Why: Warm, cozy atmosphere. Inviting color palette.
Study: The overall vibe. How the world feels like a place you want to spend time in.

### Films and Documentaries (Mood and Atmosphere)

**The Pixar Story** (Leslie Iwerks, 2007)
Why: The definitive reference for animation studio environments. Actual footage of Pixar's offices, render farms, storyboard rooms.
Study: Everything. The warmth of the spaces. The creative chaos of the storyboard rooms. The hum of the render farm. This is the world we're depicting.

**Ratatouille** (Pixar, 2007)
Why: The kitchen scenes — a creative workspace with warmth, urgency, and craft.
Study: The lighting in Gusteau's kitchen. The way the space feels functional and beautiful. The warm color palette.

**Spider-Man: Into the Spider-Verse** (Sony, 2018)
Why: The art direction of Miles's bedroom, the graffiti art, the sense of creative space.
Study: How personal spaces convey personality. The warmth and texture.

**Mad Men** (TV series, 2007-2015)
Why: Period-authentic production design. The evolution of office aesthetics from the 1960s to 1970s. Attention to detail in props and set dressing.
Study: How spaces change over time. The small details (desk objects, wall art, technology) that anchor an era.

**Halt and Catch Fire** (TV series, 2014-2017)
Why: Period tech aesthetics (1980s-1990s). The warmth of creative collaboration spaces.
Study: The computer labs, the offices, the sense of technological evolution.

### Art and Design Movements

**Mid-Century Modern Design**
Why: The aesthetic of 1950s-1970s furniture and office design — clean lines, warm wood, functional beauty.
Study: The Eames lounge chair, Danish modern furniture, the aesthetics of a 1960s design studio. FRAMEWAR's studio should feel like a place where mid-century modern meets 1990s tech.

**Saul Bass Title Sequences**
Why: Graphic design pioneer. Clean shapes, bold colors, kinetic typography.
Study: The way Bass used simple shapes to create visual impact. The FRAMEWAR logo and title screens should channel this energy.

**Bauhaus Poster Design**
Why: Functional typography, clear hierarchy, geometric shapes.
Study: The balance of type and shape. The clarity of communication.

**Illustration: Charley Harper**
Why: Simplified, geometric animal illustrations with warmth and personality.
Study: The shape language. How complex subjects are reduced to essential forms without losing character.

### Music and Audio References (For Sound Designer)

**Whiplash** (Soundtrack, 2014)
Why: The intensity of creative pressure. The sound of ambition and obsession.
Use: The tense moments when a production is in crisis or a release is bombing.

**The Social Network** (Trent Reznor & Atticus Ross, 2010)
Why: Electronic textures, driving rhythms, the sound of late-night work.
Use: The render farm at 2 AM. The sound of machines and ambition.

**Her** (Owen Pallett & William Butler, 2013)
Why: Warm, intimate, melancholic. The sound of reflection and human connection.
Use: The quieter moments. The filmography shelf. The end-of-campaign retrospective.

**Up** (Michael Giacchino, 2009)
Why: Emotional swells, playful motifs, the sound of heartfelt storytelling.
Use: The moments of triumph. Winning an award. A film succeeding beyond expectations.

**Jazz Standards (Gershwin, Ellington)**
Why: Mid-century American optimism and creativity.
Use: The early era (1995-1998). The sound of the industry before the pressure ramped up.

---

## 10. TECHNICAL CONSTRAINTS SUMMARY

### Platform and Engine

**Primary Platform**: PC (Steam)
**Secondary Platforms**: Nintendo Switch, Potential iPad port

**Engine**: Unity or Godot (recommend Unity for broader asset pipeline support and performance profiling tools)

**Rendering**: 2D assets in a 3D space (isometric perspective). Not full 3D models — flat cards and illustrated elements arranged in 3D depth.

### Resolution and Performance Targets

**Base Resolution**: 1920x1080 (16:9)
**Minimum Supported**: 1366x768
**Maximum Supported**: 4K (3840x2160)

**Frame Rate Target**: 60fps (non-negotiable for UI responsiveness)
**Minimum Frame Rate**: 30fps (acceptable on lower-end hardware, but 60fps is ideal)

**Performance Budget**:
- Draw calls: <100 per frame (UI batching required)
- Texture memory: <500MB total for UI and studio assets
- Animated elements: Max 30 simultaneous (render farm monitors, progress bars, particles)

### Asset Specifications

**UI Assets**: PNG or SVG
**Resolution**: 2x base resolution (design at 3840x2160, display at 1920x1080)
**Bit Depth**: 32-bit RGBA for transparency support
**Compression**: Lossless PNG for UI, atlas packing for performance

**Environmental Art**: PNG
**Resolution**: Per-asset, max 1024x1024 for individual objects
**Atlasing**: All UI elements packed into 2048x2048 atlases (one for buttons/icons, one for cards, one for portraits)

**Character Portraits**: PNG, 512x512 base, 1024x1024 export for retina

**Icons**: SVG preferred (scalable), PNG fallback at 64x64 (2x = 128x128 export)

### Animation Constraints

**Frame Rate**: 60fps for UI, 30fps acceptable for ambient effects
**Easing**: Cubic-bezier curves for smoothness
**Duration Limits**: <800ms for functional UI, 1-2 seconds for cinematic moments only
**Simultaneous Animations**: Max 30 (see performance budget)

### Text and Localization

**Font Format**: TrueType (.ttf) or OpenType (.otf)
**Character Set**: Latin Extended, Cyrillic (if needed), CJK fallback
**Minimum Text Size**: 14px body, 16px preferred
**Line Height**: 1.4em minimum for readability

**Text Expansion**: UI must accommodate 30-40% expansion for German/French
**Solution**: Flexible button widths, text wrapping in card bodies, ellipsis truncation for overflows with tooltips

### Accessibility

**Colorblind Support**: Icon + color pairing for all reputation systems
**Text Contrast**: WCAG AA compliance (4.5:1 contrast ratio for body text)
**UI Scaling**: Option to increase UI scale 110%, 125%, 150% for vision accessibility
**Keyboard Navigation**: Full keyboard support for all clickable elements (tab navigation, enter to confirm)

### Audio Integration

**Music Format**: OGG or MP3, stereo, 44.1kHz
**SFX Format**: WAV for short effects, OGG for longer loops
**Dynamic Music**: Layered stems (base + intensity layers) that cross-fade based on game state
**Diegetic Sound**: Render farm hum, coffee machine, pencil scratches, film projector whir

### Build Size Target

**Initial Build**: <2GB (manageable for Steam, reasonable for Switch)
**Asset Optimization**: Compress textures, use atlases, avoid duplicate assets
**Streaming**: Music and ambient audio streamed, not loaded into memory all at once

---

## 11. PRODUCTION PIPELINE VISUAL DESIGN DEEP-DIVE

This is the most important UI in the game. It deserves its own section.

### The Board Structure

**Physical Dimensions** (in-game):
The board is 3 meters wide, 1 meter tall. Mounted on the wall at eye level.

**Divisions**:
Six vertical sections of equal width, each labeled at the top:

1. **DEV** (Development) — Purple accent stripe
2. **PRE** (Pre-Production) — Amber accent stripe
3. **PROD** (Production) — Blue accent stripe
4. **POST** (Post-Production) — Teal accent stripe
5. **MKT** (Marketing) — Green accent stripe
6. **REL** (Release) — Gold accent stripe

Accent stripes are 8px tall, running the full width of each section at the top edge.

**Background**: Corkboard texture. Metal frame holding the board.

### Film Cards (The Core Element)

Each active film is represented by a card. The card moves left-to-right through the pipeline.

**Card Dimensions**: 240px wide x 140px tall (16:9 landscape rectangle)
**Card Material**: Paper texture, slight shadow (4px offset, 30% opacity)
**Pin**: A colored thumbtack at the top center of the card. Pin color indicates reputation trajectory:
- Gold pin: Film trending toward PRESTIGE
- Green pin: Film trending toward COMMERCIAL success
- Blue pin: Film showcasing TECHNICAL INNOVATION
- Purple pin: Film is high ARTISTIC COURAGE
- Gray pin: Neutral/balanced

**Card Content**:
- **Top**: Film title (bold, 18px)
- **Center**: Director portrait (small circle, 48px diameter)
- **Below portrait**: Current phase progress (circular progress ring, fills clockwise as quarters pass)
- **Bottom**: Budget status indicator (three states):
  - Green checkmark: On budget
  - Amber warning icon: Approaching overrun
  - Red alert icon: Over budget

**Hover State**: Card raises slightly (shadow increases to 6px offset), entire card brightens 10%.

**Click Action**: Card expands into a detailed view overlay showing current phase decisions, Film DNA scores so far, and decision prompts.

### Phase Labels

At the top of each section, large clear labels:

**Typography**: Bold, 20px, all-caps
**Color**: Charcoal Gray `#3D3D3D` on the Warm Cream background of the label strip
**Icons**: Each phase has a small icon next to the label:
- DEV: Pencil
- PRE: Storyboard frame
- PROD: Render farm/computer
- POST: Effects/lighting bolt
- MKT: Megaphone
- REL: Ticket/box office

### Progress Indicators

Each card shows phase progress as a circular ring around the director portrait.

**Visual**: A 48px diameter circle. The outer ring fills clockwise from 12 o'clock.
**Color**: Accent color matching the current phase (purple for DEV, amber for PRE, blue for PROD, etc.)
**Fill**: 0% at phase start, 100% at phase complete
**Animation**: Fills smoothly as in-game quarters pass

When a phase completes, the card animates: it slides right to the next section over 500ms with a subtle whoosh sound.

### Budget Status

Bottom-right corner of each card: a small icon indicating budget health.

**Three States**:
1. **Green Checkmark**: Budget on track. No action needed.
2. **Amber Warning Triangle**: Budget within 10% of overrun. Attention recommended.
3. **Red Alert Circle**: Budget overrun. Crisis state.

**Icon Size**: 24x24px
**Placement**: 8px margin from bottom-right corner

### Multi-Film Layout

When 2-3 films are active simultaneously, they stack vertically within their respective phase columns.

**Spacing**: 16px vertical margin between cards
**Overflow**: If more than 3 films are in the same phase (unlikely but possible), the section scrolls vertically.

**Visual Clarity**: Each card is visually distinct (different title, different director portrait, different pin color if applicable). The player can differentiate at a glance.

### Interactivity Flow

1. **Player views the pipeline board**: All active films are visible in their current phases.
2. **Player clicks a film card**: The card expands into an overlay (see Section 12 for overlay design).
3. **Player makes phase decisions**: Choices presented in the overlay.
4. **Player confirms**: Overlay closes. Card updates to reflect new state (progress advances, budget status may change).
5. **Time passes**: As quarters elapse, progress rings fill. When a phase completes, the card slides to the next section automatically.

### The Emotional Design Goal

When the player looks at the production pipeline board, they should feel:

1. **Control**: I can see everything happening. I know where my films are.
2. **Urgency**: Films are moving. Decisions are pending. The machine is running.
3. **Pride**: These cards represent films I greenlit. This board is my studio's heartbeat.

The board is not a spreadsheet. It's a mission control center. It should look and feel like the nerve center of a creative operation.

---

## 12. DECISION OVERLAY DESIGN

When the player clicks into a film card, an overlay appears with phase-specific decisions.

### Overlay Structure

**Background**: A large panel (800px wide x 600px tall) appears centered on screen. The studio behind it dims to 40% opacity.

**Panel Material**: Same paper texture as film cards, but larger. Pinned to the dimmed background with four thumbtacks (one at each corner). This maintains the diegetic aesthetic — the overlay is a "larger document" pinned in front of the scene.

**Close Button**: Top-right corner, a simple X icon. Or the player can click outside the panel to close.

### Content Layout

**Header** (top 100px of the panel):
- Film title (large, bold, 28px)
- Director portrait and name (left side, 64px portrait)
- Current phase name and progress (right side, "PRE-PRODUCTION — 2/3 Quarters Complete")

**Body** (middle 400px of the panel):
Phase-specific decision prompts. Each decision is presented as a card within the overlay.

**Decision Card Structure**:
- Title of the decision (e.g., "Storyboard Revision Request")
- Description (narrative text explaining the situation)
- Consequences (clear, numeric: "Cost: +$3M, Time: +1 Quarter, STORY DEPTH +0.5")
- Current context (e.g., "Current STORY DEPTH: 6.2, Current Budget: $77M")
- Two buttons: "Approve" (green) and "Decline" (red), or variations depending on the decision

**Footer** (bottom 100px of the panel):
- Current Film DNA preview (small bar graph showing STORY DEPTH, ANIMATION QUALITY, etc., as they stand so far)
- "More Info" button (opens a tooltip or sub-panel with detailed stats)

### Example Decision

**Title**: "Director Requests Dream Sequence in Act 2"

**Description**:
"Your director believes a surreal dream sequence will deepen the protagonist's emotional arc. The sequence will require an additional quarter in pre-production and $3M for complex storyboarding, but it could significantly boost the film's HEART score."

**Consequences**:
- **Cost**: +$3M
- **Time**: +1 Quarter (Pre-Production extended)
- **Impact**: HEART +0.5, ORIGINALITY +0.3
- **Risk**: Director morale -10 if declined

**Current Context**:
- **Budget**: $60M / $70M (room to absorb $3M)
- **HEART Score**: 5.8 (would become 6.3)
- **Director Morale**: 72 (healthy)

**Buttons**:
- **Approve** (green button, left): "Support the vision" — executes the decision
- **Decline** (red button, right): "Keep the schedule" — rejects the request

**Result**: Player clicks "Approve." The overlay closes. Film card on the pipeline board updates: progress ring resets slightly (1 extra quarter added), budget indicator shifts from green checkmark to amber warning (getting closer to cap). The player feels the weight of the decision.

---

## 13. BOX OFFICE GAUNTLET SCREEN DESIGN

When a film releases, the player watches the box office results in the Screening Room.

### The Screen

**Setting**: The screening room (dark, intimate, focused).

**Visual**: The projection screen shows a large LED-style display. Think: a digital scoreboard at a sports arena, but for box office numbers.

**Content**:

**Week 1 (Opening Weekend)**:
- Large number counting up from $0 to the opening weekend gross over 2 seconds (dramatic reveal)
- Below: "Opening Weekend" label
- Below: Comparison to projections ("Projected: $38M | Actual: $42M" in green if beating, red if missing)

**Week 2-4**:
- Each week, the new weekly gross displays
- Running total updates
- Drop-off percentage shown ("Week 2: -52% from opening")
- Word-of-mouth indicator: a simple bar (green = positive buzz, amber = mixed, red = negative)

**Bottom of Screen**:
- Projector Score (critic review aggregation): "Projector Score: 78/100" in gold
- Audience Score: "Audience Score: 82/100" in green
- Competing films (if any): Small ticker at the bottom showing rival releases and their numbers

**End of Week 4**:
- Final domestic gross revealed
- International multiplier applied: "International: $195M"
- Total gross: "$333M Worldwide"
- Profit calculation: "Budget: $90M | Total Gross: $333M | Studio Share: $130M | Profit: $40M"

**Visual Style**: The LED display uses Commercial Green for positive numbers, Crisis Red for losses. The numbers are bold, high-contrast, immediately readable.

**Sound Design**: Electronic counting sounds as numbers roll up. A chime when the final total locks in. Applause sound effect if the film is a hit. Silence if it bombs.

### Awards Season Notification

If the film is eligible for awards (released Q3-Q4), a notification appears after the box office screen:

**Visual**: A gold envelope icon appears on screen.

**Text**: "This film is eligible for the Academy Awards. Nomination announcements in [X] quarters."

Later, when nominations are announced, a similar screen appears:
- Gold spotlight on the screening room screen
- Text: "TIDEWALKER has been nominated for Best Animated Feature."

If the film wins:
- Gold confetti effect (subtle, not overwhelming)
- Oscar trophy icon fades in
- Text: "WINNER — Best Animated Feature"
- The trophy is added to the filmography shelf next to the film's box

---

## 14. FILMOGRAPHY SHELF DETAILED DESIGN

The endgame. The legacy display.

### Physical Structure

**Location**: Studio lobby, visible from the default camera position.

**Dimensions**: 2 meters wide, 5 shelves (expandable as more films release).

**Material**: Glass shelves on brushed metal frame. Warm spotlight from above.

### Film Box Design

Each released film is represented as a physical media box:
- **1995-2000**: VHS clamshell case
- **2001-2005**: DVD case
- **2006-2010**: Blu-ray case

The box art is procedurally generated based on Film DNA:
- **High SPECTACLE**: Dynamic action pose or explosion visual
- **High HEART**: Character-focused, emotional composition
- **High HUMOR**: Bright colors, playful character arrangement
- **High ORIGINALITY**: Abstract or stylized design

**Box Art Template**: A 3:4 vertical rectangle with:
- Film title at top (large, bold)
- Key art in center (procedurally assembled from genre/tone tags)
- Studio logo at bottom (the player's studio name)
- Rating icon (G, PG, PG-13 equivalent)
- Small text: "Winner — Best Animated Feature" if applicable

### Shelf Arrangement

Films are arranged left-to-right in release order.

**Spacing**: 8px between boxes.

**Lighting**: Each box has a subtle spotlight from above, creating a warm glow and slight reflection on the glass shelf.

### Awards Display

Next to each film box, awards are displayed:
- **Oscar Statue**: A small gold trophy (3D-modeled or illustrated, 32px tall) next to films that won Best Animated Feature
- **Critic Trophy**: A silver trophy next to films with Projector Score 85+
- **Audience Favorite**: A green ribbon next to films with Audience Score 90+

### Interactivity

**Hover**: Film box tilts slightly forward. A tooltip appears showing:
- Film title
- Director
- Total gross
- Projector Score
- Audience Score
- DNA scores (bar graph)

**Click**: A detailed retrospective panel opens (see Section 15).

### Emotional Goal

When the player looks at the filmography shelf, they should feel the weight of their career. Each box is a decision tree collapsed into a single artifact. Some boxes glow with awards. Some are commercial hits. Some are cult classics. Together, they tell a story.

This is the score. This is the game's final statement.

---

## 15. END-OF-CAMPAIGN RETROSPECTIVE SCREEN

The campaign ends in 2010. The player's final film releases. The retrospective begins.

### Screen Structure

**Setting**: The screening room, but the camera pulls back to show the entire studio.

**Visual Sequence**:
1. **Fade to black** from the final film's box office screen.
2. **Text appears**: "Fifteen years. [X] films. This is your legacy."
3. **Camera pulls back**: The studio is shown in full. The filmography shelf glows. The production pipeline board is empty (no active films). The render farm is dark. The storyboard room is quiet.
4. **Cut to the filmography shelf**: Each film box is highlighted in sequence, with a voiceover (text-only, not audio voiceover) summarizing the film.

**Voiceover Text** (procedurally generated):

"TIDEWALKER (2003) — A technical marvel that pushed CG rendering to new heights. It earned $333M worldwide and won the Oscar for Best Animated Feature. Critics called it 'a watershed moment for animation.'"

"FOLDED (2005) — A commercial disappointment, but a film your director still calls their masterpiece. It found an audience on home video and is now considered a cult classic."

[Continues for each film]

5. **Studio Stats Screen**: A summary page with:
   - Total films produced
   - Total box office (worldwide)
   - Awards won
   - Reputation profile (the four axes displayed as a radar chart)
   - Studio Soul position (revealed for the first time): "You built an Auteur Studio — a place where artists thrived and vision mattered."

6. **Final Text**: A procedurally generated "legacy statement" based on the player's choices:

**Example (for a prestige-focused player)**:
"You didn't build the biggest studio. You built a studio that mattered. Critics will remember your films. Artists wanted to work for you. You proved that animation could be art."

**Example (for a commercial-focused player)**:
"You built an empire. Your films dominated the box office. You understood the market better than anyone. You proved that animation could be a business."

**Example (for a balanced player)**:
"You balanced art and commerce. You made films that moved audiences and made money. You built something sustainable. You proved that you didn't have to choose."

7. **Credits roll**: The game's credits, with the player's filmography displayed alongside.

8. **Final shot**: The studio at night, lights off, empty. The camera holds on the filmography shelf, glowing softly. Fade to black.

### Emotional Design Goal

The retrospective is not a "score screen." It's a reflection. The player should feel:

- **Accomplishment**: I made this. These films exist because of me.
- **Regret**: I wish I'd done that differently. I wonder what would have happened if...
- **Satisfaction**: This is what I wanted to build. I did it.

The retrospective validates every choice. There are no "wrong" filmographies. Only different ones. The player's studio is theirs. The shelf is the proof.

---

## 16. MARKETING ASSETS VISUAL GUIDE

### Steam Capsule Image (Main Store Header)

**Dimensions**: 460px x 215px

**Composition**:
- **Foreground**: The production pipeline board, angled slightly, showing 2-3 film cards in various phases. Pins are visible. Warm lighting.
- **Mid-ground**: A desk with a coffee cup, a director's portrait card, and scattered storyboards.
- **Background**: The render farm, glowing teal-blue, slightly out of focus.
- **Text Overlay**: "FRAMEWAR" in bold, clean sans-serif. Subtitle: "Build Your Animation Legacy."
- **Color Palette**: Warm browns and creams, with pops of gold/green/blue from the reputation system.

**Goal**: Communicate "animation studio management" in a single image. The production board is the hook. The warm lighting is the vibe.

### Steam Library Hero Image

**Dimensions**: 3840px x 1240px

**Composition**:
Wide shot of the studio at night. Multiple rooms visible: greenlight office on the left, production pipeline board center, render farm right, screening room background. Warm lights in the office, blue glow from the render farm. The filmography shelf is visible in the distance, glowing under spotlights.

**Text Overlay**: "FRAMEWAR" large, centered. No subtitle needed — the image tells the story.

**Goal**: Sell the atmosphere. This is a place you want to be. Warm, creative, purposeful.

### Trailer Stills and GIFs

**Key Moments to Capture**:

1. **The Greenlight Moment**: A hand (implied, not shown) stamping a film concept card with "GREENLIT." The card glows and slides onto the production pipeline board. (GIF loop: 3 seconds)

2. **The Production Board in Action**: Camera pans across the board. Three films in different phases. Progress rings fill. One card slides from PRE to PROD. (GIF loop: 5 seconds)

3. **The Storyboard Room**: Camera focuses on a wall of pinned storyboards. An artist's hand pins a new frame. The wall feels alive. (Still or short GIF)

4. **The Box Office Reveal**: Screening room. The LED display counts up: "$42M Opening Weekend." The number locks in. Green checkmark appears. (GIF: 3 seconds)

5. **The Filmography Shelf**: Camera slowly pans across the shelf. 8 film boxes, some with Oscar trophies next to them. Warm lighting. (Still or slow pan GIF)

**Visual Style**: In-game footage. No UI overlays. Let the diegetic interface speak for itself.

### Logo Design

**Primary Logo**: "FRAMEWAR" in bold, geometric sans-serif. Clean, modern, slightly retro (nods to mid-century design).

**Color**: Charcoal Gray `#3D3D3D` on light backgrounds, Warm Cream `#F5E6D0` on dark backgrounds.

**Icon/Symbol**: A simplified film strip or clapperboard, integrated into the "A" in "FRAMEWAR" (the horizontal bar of the A becomes a film strip). Subtle, not gimmicky.

**Alternate**: The four reputation colors (gold/green/blue/purple) as accent stripes beneath the wordmark. This ties the logo to the game's color system.

**Usage**: Logo appears on the title screen, marketing materials, Steam page header.

---

## 17. FINAL VISUAL MANIFESTO

### What This Game Looks Like

FRAMEWAR looks like a place. Not a menu system. Not an abstract dashboard. A studio where art is made. The player walks into the greenlight office and sees a desk covered in concept cards. They walk to the production pipeline board and see their films moving through phases. They walk to the render farm and feel the hum of machines working through the night. They walk to the screening room and watch the box office numbers roll in. They walk to the filmography shelf and see their legacy on display.

Every UI element is an object. Every decision is a physical act. The player doesn't click a button labeled "Approve Storyboard Revision" — they click a pinned storyboard panel and see a thumbtack shift from red to green.

The visual language is warm, tactile, and human. The color palette leans into browns, creams, and warm lamplight, with strategic pops of gold, green, blue, and purple for the reputation system. The typography is clean and readable. The animations are purposeful and subtle. The atmosphere is "animation studio at 2 AM" — warm, focused, alive with creative energy.

### What This Game Feels Like

Looking at a screenshot of FRAMEWAR, the player should feel:

1. **Invited**: This is a space I want to enter. It looks warm and purposeful.
2. **Capable**: I can parse this screen in two seconds. I know what matters.
3. **Excited**: I want to greenlight a film. I want to see my filmography shelf fill up. I want to win an Oscar.

The art direction serves the fantasy: you are a studio head. You make films. Your decisions matter. The studio is your canvas. The filmography shelf is your scorecard.

### The Three Non-Negotiables

If the art team delivers on only three things, it must be these:

1. **The Production Pipeline Board is immediately readable**: Any player can look at it and understand film status, phase progression, and urgency in 2 seconds.

2. **The Studio feels like a place, not a UI**: The diegetic aesthetic is the identity. No floating menus. Everything is an object in space.

3. **The Four Reputation Colors (Gold/Green/Blue/Purple) are the visual spine**: They appear everywhere, consistently, creating a color-coded language the player internalizes.

If we achieve those three, the rest is refinement. If we fail any of those three, the visual identity has failed.

---

## 18. PRODUCTION CHECKLIST

Before art production begins, the following must be locked:

- [ ] **Color palette final approval**: All hex values confirmed, tested for colorblind accessibility.
- [ ] **Shape language documented**: Card dimensions, icon sizes, grid system (8px) locked.
- [ ] **Typography selected**: Font family chosen, type scale defined, licensing confirmed.
- [ ] **Portrait style reference**: 3-5 example portraits created and approved.
- [ ] **Studio layout 3D blockout**: Basic geometry of all rooms, camera angles tested.
- [ ] **Production pipeline board prototype**: Interactive mockup built, tested for readability.
- [ ] **Animation timing reference**: Easing curves and durations documented.
- [ ] **Sound design brief written**: Based on this art direction, describing the audio atmosphere.

Once these are locked, full asset production can begin.

---

**Art Direction by PIXEL**
**For FRAMEWAR — An Animation Studio Management Sim**
**February 7, 2026**

Every pixel earns its place on screen. Readability over beauty. The studio is the UI. The filmography is the score.

Show me, don't tell me.

---

**DOCUMENT COMPLETE**

This art direction document is production-ready. Hand this to an art team, and they have everything they need: color palettes with hex values, shape language rules, style do's and don'ts, asset pipeline specifications, readability tests, reference lists, and technical constraints. The vision is clear. The execution is theirs.

Now build the studio. Make it feel like a place where something beautiful was made.
