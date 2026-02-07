# FRAMEWAR — Technical Architecture Document

**Project**: FRAMEWAR (Animation Studio Simulation)
**Author**: BYTE, Lead Programmer
**Version**: 1.0
**Date**: 2026-02-07
**Status**: Production-Ready Architecture

---

## 1. ENGINE/FRAMEWORK RECOMMENDATION

### 1.1 Core Technology: Unity

Ship it on Unity. Not because Unity is perfect. Because Unity is proven for exactly this game.

**Rationale:**

- **2D/UI-Heavy**: This game IS its UI. The diegetic studio interface — corkboards, storyboard rooms, screening rooms, render farm monitors — is rendered 2D with depth layers. Unity's Canvas system + Timeline handles this cleanly. Godot could do it. Unreal can't justify the overhead.
- **Multi-Platform Day One**: Steam primary, but Switch and iPad are stretch goals per the pitch. Unity's cross-platform build pipeline ships working builds on all three. No custom tooling. The input abstraction (mouse, touch, controller) is baked in.
- **Tooling Ecosystem**: The production pipeline board, the tech tree editor, the film concept generator — these are Unity Editor tools. Custom inspectors, ScriptableObjects, and EditorWindow give you a content creation pipeline without building a bespoke editor. You'll need content authoring for 100+ film concepts, 50+ tech nodes, and procedural review templates. Unity Editor is your content tools budget.
- **Performance Is Not The Bottleneck**: This is a UI-driven sim with zero real-time 3D rendering. Your hottest loop is quarterly budget recalculation and Film DNA scoring. That's spreadsheet math, not frame-rate critical. C# is fast enough. Unity's .NET runtime handles it. If you hit perf issues, you're doing something catastrophically wrong.
- **Asset Store Pragmatism**: DOTween for UI animation, TextMesh Pro for rich text formatting, NodeCanvas for Director/Rival AI behavior trees. Don't reinvent easing curves or dialogue trees. Buy them, ship the game.

**What Unity Doesn't Give You:**

- Custom data pipeline for the simulation state machine. You'll build that.
- Save/load system for deep simulation state. You'll build that.
- Procedural content generation (film concepts, reviews). You'll build that.

That's fine. Those are game-specific systems. Unity gives you the render/platform layer. You focus on simulation depth.

**Rejected Alternatives:**

- **Godot**: Viable but immature multi-platform tooling. Switch export is community-maintained. iPad export exists but Unity's is production-tested. Godot's editor scripting is weaker for content tools. You'd save $0 (Unity Personal is free under $200k revenue) and lose 6 weeks building export pipelines.
- **Unreal**: Overkill. You don't need nanite or lumen for a corkboard interface. Blueprint is slower to iterate than C# for data-heavy simulation logic. UMG (Unreal's UI system) is a nightmare for complex nested layouts. Hard no.
- **Custom Engine**: I've made this mistake. You'll spend 18 months on windowing, input, asset loading, and build systems. The game never ships. Don't.

**Version Target**: Unity 2022.3 LTS. Stable. Well-documented. Asset Store compatibility. Don't chase Unity 6 features you don't need.

---

## 2. CORE SYSTEMS ARCHITECTURE

### 2.1 High-Level Component Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                    FRAMEWAR RUNTIME                          │
├─────────────────────────────────────────────────────────────┤
│  Presentation Layer (Unity MonoBehaviours + UI)             │
│  ┌──────────────┐ ┌──────────────┐ ┌───────────────┐       │
│  │ Studio View  │ │ Pipeline UI  │ │ Review Screen │       │
│  │ Manager      │ │ Controllers  │ │ Generator     │       │
│  └──────────────┘ └──────────────┘ └───────────────┘       │
├─────────────────────────────────────────────────────────────┤
│  Gameplay Layer (C# Services, Stateless)                    │
│  ┌──────────────┐ ┌──────────────┐ ┌───────────────┐       │
│  │ GameLoop     │ │ EventBus     │ │ InputRouter   │       │
│  │ Controller   │ │              │ │               │       │
│  └──────────────┘ └──────────────┘ └───────────────┘       │
├─────────────────────────────────────────────────────────────┤
│  Simulation Layer (C# Logic, No Unity Dependencies)         │
│  ┌──────────────┐ ┌──────────────┐ ┌───────────────┐       │
│  │ StudioState  │ │ FilmSimulator│ │ TalentManager │       │
│  │              │ │              │ │               │       │
│  └──────────────┘ └──────────────┘ └───────────────┘       │
│  ┌──────────────┐ ┌──────────────┐ ┌───────────────┐       │
│  │ EconomyCalc  │ │ RivalAI      │ │ TechTree      │       │
│  │              │ │              │ │               │       │
│  └──────────────┘ └──────────────┘ └───────────────┘       │
├─────────────────────────────────────────────────────────────┤
│  Data Layer (Pure C# Structs/Classes, Serializable)         │
│  ┌──────────────┐ ┌──────────────┐ ┌───────────────┐       │
│  │ Studio       │ │ Film         │ │ Talent        │       │
│  │ (state)      │ │ (state)      │ │ (state)       │       │
│  └──────────────┘ └──────────────┘ └───────────────┘       │
│  ┌──────────────┐ ┌──────────────┐ ┌───────────────┐       │
│  │ GameConfig   │ │ FilmConcept  │ │ TechNode      │       │
│  │ (ScriptableO)│ │ (ScriptableO)│ │ (ScriptableO) │       │
│  └──────────────┘ └──────────────┘ └───────────────┘       │
└─────────────────────────────────────────────────────────────┘
```

**Architectural Principles:**

1. **Simulation Logic Is Unity-Agnostic**: The entire simulation layer (FilmSimulator, EconomyCalc, TalentManager, etc.) is pure C# with zero `using UnityEngine;`. This enables:
   - Headless unit testing of all game logic without spinning up Unity.
   - Deterministic simulation for debugging ("why did this film score 7.2?").
   - Potential future use: command-line sim testing, automated balance runs.

2. **Data Is Serializable By Default**: Every state struct/class is `[Serializable]` and uses only primitive types, arrays, Lists, and Dictionaries. Save/load is a single `JsonUtility.ToJson()` call on the root StudioState. No references to Unity objects in save data.

3. **Event-Driven Communication**: UI and simulation communicate through a central EventBus. Example: FilmSimulator completes a production phase -> raises `FilmPhaseCompleted` event -> PipelineUIController listens, updates visual board -> StudioViewController listens, triggers confetti particle effect. Decoupled. No spaghetti dependencies.

4. **ScriptableObjects For Static Content**: All design-time data (film concept templates, tech tree definitions, review phrase libraries) are ScriptableObjects. Designers edit them in Unity Inspector. Code references them as readonly config. Version control treats them as text (force text serialization in Unity).

### 2.2 Data Flow (Quarter Tick Example)

```
User clicks "Advance Quarter" button
    |
    v
InputRouter.OnAdvanceQuarterClicked()
    |
    v
GameLoopController.AdvanceQuarter()
    |---> StudioState.CurrentQuarter++
    |---> For each active Film:
    |       FilmSimulator.TickProductionPhase(film)
    |         --> Apply resource allocation
    |         --> Check for phase completion
    |         --> Update Film.DNA scores based on decisions
    |         --> Raise FilmPhaseCompleted event (if complete)
    |
    |---> EconomyCalc.DeductQuarterlyCosts(studioState)
    |       --> Salaries, overhead, R&D burn
    |       --> Update StudioState.BudgetPool
    |
    |---> TalentManager.TickMorale(studioState)
    |       --> Apply morale decay/boosts
    |       --> Check for poaching attempts
    |       --> Raise TalentDeparture event (if triggered)
    |
    |---> TechTree.TickResearch(studioState)
    |       --> Decrement active research timers
    |       --> Raise TechNodeUnlocked event (if complete)
    |
    |---> RivalAI.TakeTurn(studioState)
    |       --> Rivals greenlight/release films
    |       --> Update competitive landscape
    |       --> Raise RivalFilmReleased event (if releasing)
    |
    |---> EventBus.Raise(QuarterAdvanced event)
    |
    v
PipelineUIController listens to FilmPhaseCompleted
    --> Updates production board visual (move card to next phase)
    --> Triggers phase gate decision prompt (if needed)
    |
    v
StudioViewController listens to TechNodeUnlocked
    --> Plays unlock animation on tech tree display
    --> Shows notification toast
    |
    v
EconomyUIController listens to QuarterAdvanced
    --> Refreshes budget display
    --> Flashes red if budget < $20M (warning state)
```

**Why This Architecture?**

Clean separation means you can change the presentation (swap the diegetic studio UI for a spreadsheet debug view) without touching simulation. You can run the simulation headless at 1000x speed to test late-game balance. You can serialize-test every quarter of a 60-quarter campaign in CI. The simulation is the source of truth. The UI is a view.

---

## 3. KEY GAMEPLAY SYSTEMS TECHNICAL DESIGN

### 3.1 Film Production Pipeline System

**Core Structure:**

```csharp
[Serializable]
public class Film
{
    public string FilmID; // GUID
    public string Title;
    public FilmConcept Concept; // Reference to ScriptableObject template
    public Director AssignedDirector;
    public ProductionPhase CurrentPhase;
    public int QuartersInCurrentPhase;
    public FilmDNA DNA; // 8 float scores
    public ProductionBudget Budget;
    public List<ProductionDecision> DecisionHistory; // Audit trail
    public List<string> AssignedAnimatorIDs;
    public List<VoiceActorCasting> VoiceCast;
    public TechnologyApproach TechApproach; // 2D, CG, Hybrid
    public int TargetReleaseQuarter;
    public FilmRisks Risks; // Hidden tags revealed during production
}

[Serializable]
public struct FilmDNA
{
    public float StoryDepth;      // 0-10
    public float AnimationQuality; // 0-10
    public float Humor;           // 0-10
    public float Heart;           // 0-10
    public float Spectacle;       // 0-10
    public float VoiceCastAppeal; // 0-10
    public float Originality;     // 0-10
    public float Rewatchability;  // 0-10

    public float CompositeScore(FilmDNAWeights weights)
    {
        return StoryDepth * weights.Story +
               AnimationQuality * weights.Animation +
               Humor * weights.Humor +
               Heart * weights.Heart +
               Spectacle * weights.Spectacle +
               VoiceCastAppeal * weights.VoiceCast +
               Originality * weights.Originality +
               Rewatchability * weights.Rewatchability;
    }
}

public enum ProductionPhase
{
    Development,
    PreProduction,
    Production,
    PostProduction,
    Marketing,
    Release,
    Completed
}
```

**FilmSimulator Service:**

```csharp
public class FilmSimulator
{
    private GameConfig _config;
    private System.Random _rng;

    public void TickProductionPhase(Film film, StudioState studio)
    {
        film.QuartersInCurrentPhase++;

        // Apply per-quarter resource allocation effects
        ApplyResourceEffects(film, studio);

        // Check for phase completion
        int requiredQuarters = GetRequiredQuartersForPhase(
            film.CurrentPhase,
            film.TechApproach,
            studio.TechTree
        );

        if (film.QuartersInCurrentPhase >= requiredQuarters)
        {
            CompletePhase(film, studio);
        }

        // Random event checks (director crisis, budget overrun, etc.)
        CheckForProductionEvents(film, studio);
    }

    private void CompletePhase(Film film, StudioState studio)
    {
        // Lock DNA scores that are finalized in this phase
        switch (film.CurrentPhase)
        {
            case ProductionPhase.Development:
                LockStoryDepthBase(film, studio);
                break;
            case ProductionPhase.PreProduction:
                LockVoiceCastAppeal(film);
                RevealHiddenRisk(film, riskIndex: 1);
                break;
            case ProductionPhase.Production:
                LockAnimationQuality(film, studio);
                LockSpectacleBase(film, studio);
                break;
            case ProductionPhase.PostProduction:
                ApplyPostProductionBoosts(film, studio);
                LockRewatchability(film);
                break;
            case ProductionPhase.Marketing:
                CalculateAwarenessScore(film, studio);
                break;
        }

        film.CurrentPhase++;
        film.QuartersInCurrentPhase = 0;
        EventBus.Raise(new FilmPhaseCompletedEvent(film));
    }

    private void LockStoryDepthBase(Film film, StudioState studio)
    {
        StoryArtist artist = studio.GetStoryArtistFor(film);
        Director director = film.AssignedDirector;

        float baseScore = artist.NarrativeSkill; // 1-10

        // Time investment modifier
        if (film.QuartersInCurrentPhase >= 3)
            baseScore += 0.5f; // Full development time
        else
            baseScore = Mathf.Min(baseScore, 6f); // Rushed cap

        // Director vision alignment
        if (director.SpecialtyMatches(film.Concept.Genre))
            baseScore += director.Vision * 0.1f;

        // Apply story outline choice modifier (from player decision)
        ProductionDecision outlineDecision = film.DecisionHistory
            .Find(d => d.Type == DecisionType.StoryOutlineChoice);
        if (outlineDecision != null)
            baseScore += outlineDecision.StoryDepthModifier;

        film.DNA.StoryDepth = Mathf.Clamp(baseScore, 0f, 10f);
    }

    // ... Similar methods for each DNA score lockpoint
}
```

**Decision Gate System:**

Every phase completion triggers a decision gate where the player makes 3-5 key choices. These are represented as:

```csharp
[Serializable]
public class ProductionDecision
{
    public DecisionType Type;
    public int ChosenOptionIndex;
    public string NarrativeText; // "Director wants to add dream sequence"
    public ProductionCost Cost; // Time, money, morale
    public DNAModifiers DNAImpact; // Which DNA scores change, by how much
    public long TimestampQuarter; // When decision was made
}

public struct DNAModifiers
{
    public float StoryDepthModifier;
    public float AnimationQualityModifier;
    public float HumorModifier;
    public float HeartModifier;
    public float SpectacleModifier;
    public float VoiceCastAppealModifier;
    public float OriginalityModifier;
    public float RewardabilityModifier;
}
```

**Phase Gate UI Flow:**

1. FilmSimulator raises `FilmPhaseCompletedEvent`.
2. PipelineUIController listens, pauses game time, displays decision gate modal.
3. Decision gate presents 3-5 options as narrative cards. Each card shows:
   - Narrative text wrapper ("Your director wants X")
   - Cost breakdown (time, budget, morale)
   - DNA impact preview ("+0.5 HEART, -0.3 ORIGINALITY")
4. Player selects option.
5. PipelineUIController calls `FilmSimulator.ApplyDecision(film, decision)`.
6. FilmSimulator modifies film state, logs decision to DecisionHistory.
7. Game time resumes.

**Performance Consideration:**

All DNA calculations are deterministic. No randomness in DNA scoring except ORIGINALITY variance (which uses a seeded RNG based on FilmID + quarter). This allows:
- Post-mortem screens to retroactively explain scores.
- Regression testing ("this film with these inputs ALWAYS scores 7.2 ± 0.1").
- Save/load without RNG state desync.

### 3.2 Talent Management System

**Data Structures:**

```csharp
[Serializable]
public class Director
{
    public string DirectorID;
    public string Name;
    public float Vision; // 1-10, affects ORIGINALITY and HEART ceiling
    public float Ego; // 1-10, affects interference tolerance
    public float CommercialSense; // 1-10, affects audience calibration
    public List<GenreTag> Specialties; // Epic, Comedy, Dark, Intimate, etc.
    public List<FilmCredit> TrackRecord; // Past films and their scores
    public int Loyalty; // 0-100, affects retention
    public int Morale; // 0-100, degrades with overrides
    public int SalaryDemand; // Per-film fee in millions
    public float ProfitParticipation; // 0.0-0.15 (% of net)
}

[Serializable]
public class Animator
{
    public string AnimatorID;
    public string Name;
    public float Speed; // 1-10
    public float Quality; // 1-10
    public AnimationStyle Style; // 2D, CG_Generalist, CG_Specialist
    public string SpecialistFocus; // If specialist: Fur, Lighting, Character, etc.
    public int Morale; // 0-100
    public int Salary; // Annual in thousands
    public int QuartersInCrunch; // Consecutive crunch tracking
}

[Serializable]
public class VoiceActor
{
    public string ActorID;
    public string Name;
    public float StarPower; // 1-10, affects marketing
    public float ActingQuality; // 1-10, affects performance
    public int SalaryDemand; // Per role in thousands
    public List<int> AvailableQuarters; // Scheduling windows
    public Dictionary<string, float> ChemistryModifiers; // ActorID -> modifier
    public RecentFilmPerformance LastFilm; // Success/flop affects demand
}
```

**TalentManager Service:**

```csharp
public class TalentManager
{
    public void TickMorale(StudioState studio)
    {
        foreach (var animator in studio.Animators)
        {
            // Base morale decay/regen
            if (animator.QuartersInCrunch > 0)
                animator.Morale -= 20; // Crunch penalty
            else
                animator.Morale = Mathf.Min(animator.Morale + 5, 100); // Regen

            // Check for quit threshold
            if (animator.Morale < 30 && RNG.NextFloat() < 0.15f)
            {
                studio.Animators.Remove(animator);
                EventBus.Raise(new TalentDepartureEvent(animator));
            }
        }

        // Similar for Directors (track morale, loyalty)
        foreach (var director in studio.Directors)
        {
            UpdateDirectorLoyalty(director, studio);
        }
    }

    public void CheckPoachingAttempts(StudioState studio, List<RivalStudio> rivals)
    {
        foreach (var animator in studio.Animators)
        {
            // Poaching probability based on morale + salary gap
            float marketSalary = GetMarketSalary(animator.Quality, studio.CurrentQuarter);
            float salaryGap = marketSalary - animator.Salary;
            float moraleGap = (100 - animator.Morale) / 100f;

            float poachChance = (salaryGap / marketSalary) * 0.2f + moraleGap * 0.1f;

            if (RNG.NextFloat() < poachChance)
            {
                RivalStudio poacher = ChoosePoachingRival(rivals);
                EventBus.Raise(new PoachingAttemptEvent(animator, poacher));
                // Player can counter-offer in event handler
            }
        }
    }

    public float CalculateTeamQuality(List<Animator> team)
    {
        if (team.Count == 0) return 0f;

        float totalQuality = 0f;
        int synergyPairs = 0;

        foreach (var animator in team)
        {
            totalQuality += animator.Quality;

            // Check for synergy bonuses (same style)
            int sameStyleCount = team.Count(a => a.Style == animator.Style);
            if (sameStyleCount >= 2)
                synergyPairs++;
        }

        float avgQuality = totalQuality / team.Count;
        float synergyBonus = (synergyPairs / 2) * 0.5f; // +0.5 per synergy pair

        return avgQuality + synergyBonus;
    }
}
```

**Talent Hiring Flow:**

1. Player opens Hiring UI (diegetic: "Talent Agency Board").
2. TalentManager generates available talent pool from market based on:
   - Studio reputation (high PRESTIGE attracts high-VISION directors).
   - Current quarter (talent refreshes yearly).
   - Random pool from master talent database (ScriptableObject library).
3. UI displays talent cards with attributes, salary demands, specialties.
4. Player selects talent, confirms hire.
5. TalentManager deducts hiring cost, adds to studio roster.
6. If hiring a Director/Animator mid-production, check for conflicts with assigned Directors (ego clashes).

**Crunch Mechanics:**

Crunch is activated per-film, per-quarter during Production phase:

```csharp
public void ActivateCrunch(Film film, StudioState studio)
{
    List<Animator> assignedTeam = studio.GetAnimatorsAssignedTo(film);

    foreach (var animator in assignedTeam)
    {
        animator.Speed += 2f; // Boost speed
        animator.Morale -= 20; // Morale cost
        animator.QuartersInCrunch++;

        // Studio-wide culture penalty after 3 consecutive quarters
        if (animator.QuartersInCrunch >= 3)
        {
            studio.StudioCulturePenalty = true; // Affects future hiring costs
            EventBus.Raise(new StudioCultureCrisisEvent());
        }
    }
}
```

**Design Note:** Crunch is mechanically viable short-term but punishing long-term. It's a loan against the future. The game doesn't moralize — it just makes the costs explicit.

### 3.3 Technology Tree System

**Data Structure:**

```csharp
[CreateAssetMenu(fileName = "TechNode", menuName = "FRAMEWAR/TechNode")]
public class TechNode : ScriptableObject
{
    public string NodeID;
    public string DisplayName;
    public string Description;
    public TechBranch Branch; // CG, 2D, Hybrid
    public int ResearchCostMillions;
    public int ResearchQuarters;
    public List<string> PrerequisiteNodeIDs; // Must be unlocked first
    public TechEffects Effects;
}

[Serializable]
public struct TechEffects
{
    public float AnimationQualityFloorBoost;
    public float AnimationQualityCeilingBoost;
    public float SpectacleBoost;
    public float HeartCeilingBoost; // For facial rigging nodes
    public float OriginalityBoost; // For stylized rendering
    public int ProductionQuartersReduction; // Real-time preview node
    public int RenderFarmEfficiencyBoost; // Percentage
    public List<string> UnlockedVisualTags; // "Fur", "FluidDynamics", etc.
}

[Serializable]
public class TechTreeState
{
    public List<string> UnlockedNodeIDs;
    public List<TechResearchProgress> ActiveResearch;
}

[Serializable]
public struct TechResearchProgress
{
    public string NodeID;
    public int QuartersRemaining;
    public int TotalCostPaid; // In millions
}
```

**TechTree Service:**

```csharp
public class TechTree
{
    private List<TechNode> _allNodes; // Loaded from ScriptableObject database

    public void TickResearch(StudioState studio)
    {
        for (int i = studio.TechTreeState.ActiveResearch.Count - 1; i >= 0; i--)
        {
            var research = studio.TechTreeState.ActiveResearch[i];
            research.QuartersRemaining--;

            if (research.QuartersRemaining <= 0)
            {
                TechNode node = _allNodes.Find(n => n.NodeID == research.NodeID);
                UnlockNode(node, studio);
                studio.TechTreeState.ActiveResearch.RemoveAt(i);
            }
        }
    }

    private void UnlockNode(TechNode node, StudioState studio)
    {
        studio.TechTreeState.UnlockedNodeIDs.Add(node.NodeID);

        // Apply global effects to studio capabilities
        studio.TechCapabilities.AnimationQualityFloor += node.Effects.AnimationQualityFloorBoost;
        studio.TechCapabilities.AnimationQualityCeiling += node.Effects.AnimationQualityCeilingBoost;
        // ... etc for all effects

        EventBus.Raise(new TechNodeUnlockedEvent(node));
    }

    public bool CanApplyToInProgressFilm(TechNode node, Film film)
    {
        // Retroactive tech application rule:
        // Can apply if film is in Production phase or earlier
        return film.CurrentPhase <= ProductionPhase.Production;
    }

    public void ApplyTechRetroactively(TechNode node, Film film, StudioState studio)
    {
        // Costs +$3M and +1 quarter delay
        film.Budget.TotalSpent += 3_000_000;
        film.QuartersInCurrentPhase++; // Delay

        // Node effects apply immediately to film's DNA caps
        // (calculated during next lockpoint)
    }
}
```

**Tech Tree UI:**

Render as a node graph (use Unity UI + custom line rendering or a tree layout algorithm). Each node displays:
- Name, description, cost, research time.
- Prerequisites (grey out if not unlocked).
- Current research progress bar (if active).

Player can queue one research at a time (expandable to 2 with a studio upgrade).

### 3.4 Box Office Gauntlet System

**Revenue Calculation Pipeline:**

```csharp
public class BoxOfficeSimulator
{
    private GameConfig _config;

    public BoxOfficeResult SimulateRelease(Film film, StudioState studio, List<RivalFilm> competingFilms)
    {
        BoxOfficeResult result = new BoxOfficeResult();

        // Week 1: Opening Weekend
        float openingWeekend = CalculateOpeningWeekend(film, studio, competingFilms);
        result.WeeklyGross[0] = openingWeekend;

        // Weeks 2-4: Drop-off with WOM modifiers
        float dropRate = CalculateDropRate(film);
        float womModifier = CalculateWOMModifier(film);

        for (int week = 1; week < 4; week++)
        {
            result.WeeklyGross[week] = result.WeeklyGross[week - 1] * dropRate * womModifier;
        }

        // Total domestic
        result.DomesticGross = result.WeeklyGross.Sum();

        // International multiplier
        float intlMultiplier = CalculateInternationalMultiplier(film);
        result.InternationalGross = result.DomesticGross * intlMultiplier;

        // Studio revenue share (45% domestic, 35% international)
        result.StudioShareDomestic = result.DomesticGross * 0.45f;
        result.StudioShareInternational = result.InternationalGross * 0.35f;

        // Home video (arrives 2 quarters later)
        float homeVideoPercent = Mathf.Lerp(0.3f, 0.6f, film.DNA.Rewatchability / 10f);
        result.HomeVideoRevenue = result.DomesticGross * homeVideoPercent;

        // Generate reviews
        result.ProjectorScore = CalculateProjectorScore(film, studio);
        result.AudienceScore = CalculateAudienceScore(film);
        result.CriticReviews = GenerateCriticReviews(film, result.ProjectorScore);

        return result;
    }

    private float CalculateOpeningWeekend(Film film, StudioState studio, List<RivalFilm> competing)
    {
        float dnaComposite = film.DNA.CompositeScore(_config.BoxOfficeWeights);
        float basePotential = (film.Budget.Total / 4_000_000f) * (dnaComposite / 7f);

        // Awareness multiplier
        float awarenessBoost = 0.5f + (film.Marketing.AwarenessScore / 100f);

        // Star power modifier
        float starPowerMax = film.VoiceCast.Max(v => v.Actor.StarPower);
        float starModifier = 1f + (starPowerMax * 0.03f);

        // Season modifier
        float seasonMod = GetSeasonModifier(studio.CurrentQuarter);

        // Competition modifier
        float compMod = 1f;
        if (competing.Count > 0)
            compMod = 0.7f; // 30% reduction if competing releases

        return basePotential * awarenessBoost * starModifier * seasonMod * compMod;
    }

    private float CalculateDropRate(Film film)
    {
        float baseDropRate = 0.45f; // 55% drop per week

        // HEART reduces drop (legs)
        if (film.DNA.Heart > 6f)
            baseDropRate += (film.DNA.Heart - 6f) * 0.05f;

        // REWATCHABILITY reduces drop
        if (film.DNA.Rewatchability > 6f)
            baseDropRate += (film.DNA.Rewatchability - 6f) * 0.03f;

        // SPECTACLE > STORY increases drop (frontloaded)
        float spectacleImbalance = film.DNA.Spectacle - film.DNA.StoryDepth;
        if (spectacleImbalance > 0)
            baseDropRate -= spectacleImbalance * 0.05f;

        return Mathf.Clamp(baseDropRate, 0.3f, 0.7f);
    }

    private int CalculateProjectorScore(Film film, StudioState studio)
    {
        float dnaComposite = film.DNA.CompositeScore(_config.CriticWeights);
        int baseScore = Mathf.RoundToInt(dnaComposite * 10f);

        // Originality bonus (critics reward novelty)
        int originalityBonus = Mathf.RoundToInt(film.DNA.Originality * 2f);

        // Director prestige bonus
        float directorAvg = film.AssignedDirector.TrackRecord
            .Average(credit => credit.ProjectorScore);
        int directorBonus = Mathf.RoundToInt(directorAvg * 0.15f);

        // Era alignment bonus
        int eraBonus = GetEraAlignmentBonus(film, studio.CurrentQuarter);

        // Random variance
        int variance = 0;
        if (film.DNA.Originality >= 8f)
            variance = RNG.Next(-3, 4); // High variance for bold films
        else
            variance = RNG.Next(-1, 2); // Low variance for safe films

        int finalScore = baseScore + originalityBonus + directorBonus + eraBonus + variance;
        return Mathf.Clamp(finalScore, 0, 100);
    }

    private List<CriticReview> GenerateCriticReviews(Film film, int projectorScore)
    {
        // Procedurally generate 5-10 critic reviews using phrase templates
        // Phrase selection based on DNA scores and projector score tier

        List<CriticReview> reviews = new List<CriticReview>();
        int reviewCount = RNG.Next(5, 11);

        for (int i = 0; i < reviewCount; i++)
        {
            CriticReview review = new CriticReview();
            review.CriticName = _config.CriticNames[RNG.Next(_config.CriticNames.Count)];
            review.Publication = _config.PublicationNames[RNG.Next(_config.PublicationNames.Count)];
            review.Score = projectorScore + RNG.Next(-8, 9); // Individual variance
            review.QuoteText = GenerateReviewQuote(film, review.Score);
            reviews.Add(review);
        }

        return reviews;
    }

    private string GenerateReviewQuote(Film film, int score)
    {
        // Template-based generation with DNA score conditionals
        // Example: If HEART > 8 and STORY > 7, use "emotionally devastating" template
        // If SPECTACLE > 8 and STORY < 5, use "all flash, no substance" template

        ReviewTemplate template = _config.ReviewTemplates.Find(t =>
            t.ScoreRange.Contains(score) &&
            t.DNACondition.Matches(film.DNA)
        );

        return template.GenerateQuote(film);
    }
}
```

**Box Office UI Presentation:**

The 4-week gauntlet plays out as a cinematic sequence:

1. Player clicks "Release Film" on the production board.
2. Transition to Screening Room view (diegetic space).
3. Week 1 opening weekend animates in (numbers counting up, city skyline backdrop).
4. Show competing films (if any) with their opening numbers.
5. Display 3-5 critic review quotes scrolling in (newspaper headline aesthetic).
6. Week 2-4 animate sequentially (bar chart or ticker animation).
7. Final totals display: domestic, international, studio share.
8. Projector Score badge animates in (Rotten Tomatoes style).
9. Awards eligibility check (if Q3/Q4 release, badge appears).
10. Player clicks "Continue" to return to studio view.

**Performance Note:** All box office math is front-loaded calculation, not frame-by-frame simulation. Simulate the entire 4-week run in one pass, store results, animate the presentation. Don't recalculate every frame.

---

## 4. AI/SIMULATION SYSTEMS

### 4.1 Rival Studio AI

**Rival Studio Data:**

```csharp
[Serializable]
public class RivalStudio
{
    public string StudioID;
    public string Name;
    public ReputationProfile Reputation; // 4 axes like player
    public List<RivalFilm> Filmography;
    public RivalFilm CurrentProduction; // Simplified: 1 film at a time
    public RivalStrategy Strategy; // Prestige, Commercial, Technical, Franchise
    public int BudgetPool; // Abstracted, not simulated in detail
}

public enum RivalStrategy
{
    Prestige,      // Chases awards, high ORIGINALITY
    Commercial,    // Safe sequels, high AUDIENCE BREADTH
    Technical,     // Tech showoff, cutting-edge CG
    Franchise      // Builds multi-film universes
}
```

**RivalAI Behavior:**

```csharp
public class RivalAI
{
    public void TakeTurn(StudioState playerStudio, List<RivalStudio> rivals, int currentQuarter)
    {
        foreach (var rival in rivals)
        {
            // Decision: Greenlight new film or continue current production?
            if (rival.CurrentProduction == null && ShouldGreenlightFilm(rival, currentQuarter))
            {
                RivalFilm newFilm = GenerateRivalFilm(rival, playerStudio);
                rival.CurrentProduction = newFilm;
                EventBus.Raise(new RivalGreenlightEvent(rival, newFilm));
            }

            // Advance current production
            if (rival.CurrentProduction != null)
            {
                rival.CurrentProduction.QuartersRemaining--;

                if (rival.CurrentProduction.QuartersRemaining <= 0)
                {
                    ReleaseRivalFilm(rival, playerStudio);
                }
            }

            // Attempt to poach player's talent (if aggressive)
            if (rival.Strategy == RivalStrategy.Technical && currentQuarter % 4 == 0)
            {
                TalentManager.CheckPoachingAttempts(playerStudio, new List<RivalStudio> { rival });
            }
        }
    }

    private RivalFilm GenerateRivalFilm(RivalStudio rival, StudioState playerStudio)
    {
        RivalFilm film = new RivalFilm();

        // Strategy influences film type
        switch (rival.Strategy)
        {
            case RivalStrategy.Prestige:
                film.Budget = RNG.Next(60_000_000, 110_000_000);
                film.DNA.Originality = RNG.NextFloat(7f, 10f);
                film.DNA.StoryDepth = RNG.NextFloat(7f, 10f);
                film.TargetReleaseQuarter = FindOscarSeasonQuarter(playerStudio.CurrentQuarter);
                break;
            case RivalStrategy.Commercial:
                film.Budget = RNG.Next(80_000_000, 150_000_000);
                film.DNA.Spectacle = RNG.NextFloat(7f, 10f);
                film.DNA.Humor = RNG.NextFloat(6f, 9f);
                film.TargetReleaseQuarter = FindSummerQuarter(playerStudio.CurrentQuarter);
                break;
            case RivalStrategy.Franchise:
                // Check if they have a successful film to sequel
                if (rival.Filmography.Any(f => f.DomesticGross > 150_000_000))
                    film.IsSequel = true;
                break;
        }

        // Abstracted production time
        film.QuartersRemaining = RNG.Next(12, 17); // 3-4 years

        // Check for competitive overlap with player's films
        foreach (var playerFilm in playerStudio.Films)
        {
            if (playerFilm.Concept.Genre == film.Genre &&
                Mathf.Abs(playerFilm.TargetReleaseQuarter - film.TargetReleaseQuarter) <= 1)
            {
                // Rival detected overlap — either delay or compete head-to-head
                if (rival.Reputation.Commercial > 60)
                    film.TargetReleaseQuarter = playerFilm.TargetReleaseQuarter; // Compete
                else
                    film.TargetReleaseQuarter += 2; // Dodge
            }
        }

        return film;
    }

    private void ReleaseRivalFilm(RivalStudio rival, StudioState playerStudio)
    {
        RivalFilm film = rival.CurrentProduction;

        // Simulate box office (simplified vs. player's full sim)
        float projectedGross = film.Budget * RNG.NextFloat(1.5f, 4.0f); // Wide variance
        film.DomesticGross = projectedGross;
        film.ProjectorScore = RNG.Next(40, 95);

        // Update rival reputation
        if (film.ProjectorScore > 75)
            rival.Reputation.Prestige += 5;
        if (film.DomesticGross > 200_000_000)
            rival.Reputation.Commercial += 5;

        // Add to filmography
        rival.Filmography.Add(film);
        rival.CurrentProduction = null;

        EventBus.Raise(new RivalFilmReleasedEvent(rival, film));
    }
}
```

**Design Philosophy:**

Rival AI is intentionally simplified. Full FilmSimulator depth for 3+ rival studios would balloon complexity with minimal player-visible benefit. Instead:
- Rivals greenlight and release on predictable schedules.
- Their films have abstracted DNA scores (not built from granular decisions).
- Box office results use a variance formula rather than detailed simulation.
- Rivals create strategic pressure (release timing competition, awards race) without overwhelming the player with opponent complexity.

The player should feel rivals as credible competitors, not omniscient optimizers. Rivals occasionally make "dumb" choices (releasing a prestige film in summer, greenlighting a fourth sequel) to feel human.

### 4.2 Procedural Film Concept Generation

**Concept Template Structure:**

```csharp
[CreateAssetMenu(fileName = "FilmConcept", menuName = "FRAMEWAR/FilmConcept")]
public class FilmConceptTemplate : ScriptableObject
{
    public string ConceptID;
    [TextArea(3, 6)]
    public string LoglineTemplate; // "A [PROTAGONIST] discovers [CONCEPT] in [SETTING]"
    public List<string> ProtagonistOptions;
    public List<string> ConceptOptions;
    public List<string> SettingOptions;
    public GenreTag Genre;
    public ToneTag Tone;
    public IntRange OriginalityRange; // Min/max for procedural roll
    public IntRange AudienceBreadthRange;
    public IntRange TechnicalAmbitionRange;
    public IntRange SequelPotentialRange;
    public List<HiddenRiskTag> PossibleRisks; // Pool to select from
}

public class FilmConceptGenerator
{
    private List<FilmConceptTemplate> _templates;

    public FilmConcept GenerateConcept(StudioState studio)
    {
        // Select template based on studio reputation
        // High PRESTIGE studios receive more high-ORIGINALITY concepts
        // High COMMERCIAL studios receive more high-AUDIENCE_BREADTH concepts

        FilmConceptTemplate template = ChooseTemplate(studio.Reputation);

        FilmConcept concept = new FilmConcept();
        concept.Title = GenerateTitle(template);
        concept.Logline = GenerateLogline(template);
        concept.Genre = template.Genre;
        concept.Tone = template.Tone;

        concept.Originality = RNG.Next(template.OriginalityRange.Min, template.OriginalityRange.Max + 1);
        concept.AudienceBreadth = RNG.Next(template.AudienceBreadthRange.Min, template.AudienceBreadthRange.Max + 1);
        concept.TechnicalAmbition = RNG.Next(template.TechnicalAmbitionRange.Min, template.TechnicalAmbitionRange.Max + 1);
        concept.SequelPotential = RNG.Next(template.SequelPotentialRange.Min, template.SequelPotentialRange.Max + 1);

        // Assign 1-2 hidden risks
        int riskCount = RNG.NextFloat() < 0.6f ? 1 : 2;
        concept.HiddenRisks = template.PossibleRisks
            .OrderBy(r => RNG.Next())
            .Take(riskCount)
            .ToList();

        return concept;
    }

    private string GenerateLogline(FilmConceptTemplate template)
    {
        string logline = template.LoglineTemplate;

        logline = logline.Replace("[PROTAGONIST]", ChooseRandom(template.ProtagonistOptions));
        logline = logline.Replace("[CONCEPT]", ChooseRandom(template.ConceptOptions));
        logline = logline.Replace("[SETTING]", ChooseRandom(template.SettingOptions));

        return logline;
    }

    private string GenerateTitle(FilmConceptTemplate template)
    {
        // Title generation: combine setting noun + evocative adjective
        // Or use a pre-authored title pool associated with template

        if (template.TitlePool.Count > 0)
            return ChooseRandom(template.TitlePool);

        // Fallback procedural generation
        string adjective = ChooseRandom(_config.EvocativeAdjectives);
        string noun = ChooseRandom(template.SettingOptions);
        return $"{adjective} {noun}";
    }
}
```

**Content Authoring Workflow:**

1. Designer creates 100+ FilmConceptTemplate ScriptableObjects in Unity.
2. Each template has:
   - A logline template with [VARIABLE] placeholders.
   - Lists of substitution options for each variable.
   - Attribute ranges tuned to the concept's identity.
   - Hidden risk tags that thematically fit the concept.
3. At runtime, generator selects template, fills variables, rolls attributes.
4. Result: a concept that feels authored (hand-written logline template) with variability (different attribute rolls, different variable substitutions).

**Playtest Goal:** By playthrough #3, the player should still encounter concepts that feel fresh. 100 templates × 5-10 variable permutations = 500-1000 unique-feeling concepts across repeated plays.

### 4.3 Procedural Review Generation

**Review Template System:**

```csharp
[CreateAssetMenu(fileName = "ReviewTemplate", menuName = "FRAMEWAR/ReviewTemplate")]
public class ReviewTemplate : ScriptableObject
{
    public IntRange ScoreRange; // This template applies to scores in this range
    public DNACondition DNACondition; // e.g., "HEART > 7 AND STORY > 6"
    [TextArea(2, 4)]
    public List<string> PhrasePool; // Pool of possible quote fragments
    public List<string> OpeningPhrases;
    public List<string> ClosingPhrases;
}

[Serializable]
public class DNACondition
{
    public float MinHeart;
    public float MaxHeart;
    public float MinStory;
    public float MaxStory;
    public float MinSpectacle;
    public float MaxSpectacle;
    // ... etc for all DNA attributes

    public bool Matches(FilmDNA dna)
    {
        return dna.Heart >= MinHeart && dna.Heart <= MaxHeart &&
               dna.StoryDepth >= MinStory && dna.StoryDepth <= MaxStory &&
               dna.Spectacle >= MinSpectacle && dna.Spectacle <= MaxSpectacle;
    }
}

public class ReviewGenerator
{
    public string GenerateQuote(Film film, int reviewScore)
    {
        // Find matching template
        ReviewTemplate template = _templates.Find(t =>
            t.ScoreRange.Contains(reviewScore) &&
            t.DNACondition.Matches(film.DNA)
        );

        if (template == null)
            template = _fallbackTemplate; // Ensure we always generate something

        // Construct review quote
        string opening = ChooseRandom(template.OpeningPhrases);
        string body = ChooseRandom(template.PhrasePool);
        string closing = ChooseRandom(template.ClosingPhrases);

        // Insert film title
        string quote = $"{opening} '{film.Title}' {body} {closing}";

        return quote;
    }
}
```

**Example Templates:**

**High Score + High HEART + High STORY:**
- Opening: "A masterpiece of animation,", "Transcendent storytelling,", "Rarely does a film"
- Body: "captures the ineffable beauty of", "renders emotion with breathtaking precision in", "achieves a depth uncommon in the medium with"
- Closing: "A triumph.", "Essential viewing.", "Proof that animation is art."

**High Score + High SPECTACLE + Low STORY:**
- Opening: "Visually stunning but narratively thin,", "A technical marvel that", "Gorgeous to behold,"
- Body: "dazzles the eyes while leaving the heart cold in", "showcases cutting-edge animation that can't quite mask a hollow core in", "is all spectacle, little substance, yet undeniably entertaining in"
- Closing: "Worth seeing for the visuals alone.", "A feast for the eyes, a snack for the brain.", "Impressive craft, forgettable story."

**Mid Score + High HUMOR:**
- Opening: "A serviceable comedy,", "Amusing if unremarkable,", "Kids will laugh, adults will tolerate"
- Body: "delivers enough gags to sustain interest in", "coasts on charm rather than innovation with", "plays it safe with familiar beats in"
- Closing: "Fine for a rainy afternoon.", "Harmless fun.", "Could be worse."

**Low Score:**
- Opening: "A misfire,", "Disappointingly flat,", "Wastes its premise with"
- Body: "struggles to find a reason to exist in", "collapses under its own ambitions with", "is as tedious as it is forgettable in"
- Closing: "Skip it.", "A rare stumble.", "Not even the animation can save this one."

**Content Volume:** 20-30 ReviewTemplates covering the major DNA profile archetypes. Each template has 5-8 phrases per slot. Result: hundreds of unique review combinations that contextually fit the film's profile.

---

## 5. SAVE SYSTEM DESIGN

### 5.1 Architecture

**Save Data Structure:**

The entire game state is a single serializable tree rooted at `StudioState`:

```csharp
[Serializable]
public class StudioState
{
    public string StudioName;
    public int CurrentQuarter; // 0 = 1995 Q1
    public long BudgetPool; // In dollars

    public List<Film> Films; // All films (in production, released, completed)
    public List<Director> Directors;
    public List<Animator> Animators;
    public List<StoryArtist> StoryArtists;

    public TechTreeState TechTree;
    public ReputationProfile Reputation;
    public StudioCapabilities Capabilities; // Production slots, render farm capacity

    public float StudioSoul; // -100 to +100, hidden from player

    public List<ProductionDecision> GlobalDecisionHistory; // Audit trail
    public List<RivalStudio> Rivals;

    public RandomState RNGState; // Seeded RNG state for determinism
}
```

**Save/Load Implementation:**

```csharp
public class SaveSystem
{
    private static string SaveDirectory => Application.persistentDataPath + "/Saves/";

    public void SaveGame(StudioState state, string saveName)
    {
        if (!Directory.Exists(SaveDirectory))
            Directory.CreateDirectory(SaveDirectory);

        string json = JsonUtility.ToJson(state, prettyPrint: true);
        string filePath = SaveDirectory + saveName + ".json";

        File.WriteAllText(filePath, json);

        // Also write metadata file for save slot UI
        SaveMetadata meta = new SaveMetadata
        {
            SaveName = saveName,
            StudioName = state.StudioName,
            Quarter = state.CurrentQuarter,
            BudgetPool = state.BudgetPool,
            FilmCount = state.Films.Count(f => f.CurrentPhase == ProductionPhase.Completed),
            Timestamp = DateTime.Now
        };

        string metaJson = JsonUtility.ToJson(meta);
        File.WriteAllText(filePath + ".meta", metaJson);
    }

    public StudioState LoadGame(string saveName)
    {
        string filePath = SaveDirectory + saveName + ".json";

        if (!File.Exists(filePath))
        {
            Debug.LogError($"Save file not found: {filePath}");
            return null;
        }

        string json = File.ReadAllText(filePath);
        StudioState state = JsonUtility.FromJson<StudioState>(json);

        // Restore RNG state for determinism
        RNG.RestoreState(state.RNGState);

        return state;
    }

    public List<SaveMetadata> GetAllSaves()
    {
        if (!Directory.Exists(SaveDirectory))
            return new List<SaveMetadata>();

        var metaFiles = Directory.GetFiles(SaveDirectory, "*.meta");
        List<SaveMetadata> saves = new List<SaveMetadata>();

        foreach (var metaFile in metaFiles)
        {
            string metaJson = File.ReadAllText(metaFile);
            SaveMetadata meta = JsonUtility.FromJson<SaveMetadata>(metaJson);
            saves.Add(meta);
        }

        return saves.OrderByDescending(s => s.Timestamp).ToList();
    }
}
```

**Autosave Strategy:**

- Autosave at the end of every quarter (after all systems tick).
- Keep last 3 autosaves (rolling buffer).
- Manual saves: player can save at any time, unlimited slots.
- Quicksave: dedicated slot overwritten on each quicksave (F5 keybind).

**Save Compatibility:**

Version the save format:

```csharp
[Serializable]
public class StudioState
{
    public int SaveVersion = 1; // Increment on breaking changes
    // ... rest of state
}

public StudioState LoadGame(string saveName)
{
    StudioState state = JsonUtility.FromJson<StudioState>(json);

    if (state.SaveVersion < CURRENT_SAVE_VERSION)
    {
        state = MigrateSaveData(state);
    }

    return state;
}

private StudioState MigrateSaveData(StudioState oldState)
{
    // Apply incremental migrations from oldState.SaveVersion to CURRENT_SAVE_VERSION
    // Example: Version 1 -> 2 adds StudioSoul field (default to 0)

    if (oldState.SaveVersion == 1)
    {
        oldState.StudioSoul = 0f;
        oldState.SaveVersion = 2;
    }

    // Chain additional migrations as needed

    return oldState;
}
```

**Cloud Save (Stretch Goal):**

If shipping on Steam, integrate Steamworks Cloud Save API. Unity's Steamworks.NET plugin handles this. Save to local disk as primary, sync to Steam Cloud as backup. Player can disable cloud saves in options.

---

## 6. PERFORMANCE BUDGET AND OPTIMIZATION STRATEGY

### 6.1 Target Performance

**Platform Specs:**

- **PC (Steam)**: 1080p @ 60fps on integrated graphics (Intel UHD 620 equivalent). Modest CPU (i5-8250U or equivalent).
- **Nintendo Switch**: 720p handheld / 1080p docked @ 30fps. Constrained by CPU (ARM Cortex-A57).
- **iPad (stretch)**: iPad Air 4 or newer, 60fps target.

**Performance Constraints:**

This is a UI-heavy simulation, not a 3D renderer. The bottleneck is:
- UI rendering (Canvas draw calls, text rendering).
- Simulation tick (quarterly calculations across all films, talent, rivals).
- Data serialization (save/load).

**Frame Budget (60fps = 16.6ms per frame):**

- **Rendering**: 8ms (UI draw calls, canvas batching, particle effects)
- **Simulation**: 4ms (amortized — quarterly tick is 1-frame spike, then idle)
- **Input**: 1ms
- **Overhead**: 3.6ms

### 6.2 Optimization Strategies

#### UI Rendering

**Problem:** Unity's Canvas system can tank framerate with excessive draw calls or non-batched elements.

**Solutions:**

1. **Canvas Hierarchy:**
   - Use multiple canvases for different UI layers (HUD, Studio View, Modals).
   - Static elements (background, fixed UI) on separate canvas marked "Static".
   - Dynamic elements (production board cards, animating numbers) on separate canvas.
   - This allows Unity to skip rebuilding static canvases on every frame.

2. **Sprite Atlasing:**
   - All UI sprites in a single atlas (or 2-3 atlases if exceeding max texture size).
   - Reduces draw calls from hundreds to single-digit.

3. **TextMesh Pro:**
   - Use TMP for all text. It's GPU-rasterized, orders of magnitude faster than legacy Unity Text.
   - Pregenerate font atlases for all used characters.

4. **Avoid Layout Groups At Runtime:**
   - Unity's LayoutGroup components (HorizontalLayoutGroup, GridLayoutGroup) rebuild every frame if any child changes.
   - For production board (20+ film cards), manually position cards. Update positions only when cards change state (e.g., phase transition).

5. **Particle Effects Sparingly:**
   - Confetti on award win, dust particles on render farm — fine.
   - Don't run particles continuously. Burst effects only.

#### Simulation Performance

**Problem:** Quarterly tick processes 3 active films × 6 phases × talent roster × tech tree × rival studios. Could spike to 50ms+ if naive.

**Solutions:**

1. **Amortize Work Across Frames:**
   - Don't process entire quarter tick in one frame.
   - Spread across 3-5 frames:
     - Frame 1: FilmSimulator.TickAllFilms()
     - Frame 2: TalentManager.TickMorale()
     - Frame 3: EconomyCalc.ProcessQuarterly()
     - Frame 4: RivalAI.TakeTurn()
     - Frame 5: EventBus.Flush(), UI updates
   - Show "Processing Quarter..." spinner during multi-frame tick.

2. **Cache Calculations:**
   - Film DNA composite scores are recalculated frequently (UI displays, tooltips).
   - Cache composite score in Film struct. Mark dirty flag when DNA changes. Recalculate only on dirty read.

3. **Avoid LINQ In Hot Paths:**
   - LINQ is readable but allocates garbage and is slower than manual loops for small collections.
   - Hot path example: `FilmSimulator.TickProductionPhase()` called per film per quarter.
   - Use `for` loops instead of `.Where().Select()`.

4. **Deterministic RNG:**
   - Use a seeded System.Random instance (stored in StudioState).
   - Avoids hidden allocations from `UnityEngine.Random`.

#### Save/Load Performance

**Problem:** Serializing 60 quarters of state (10+ films, 50+ talent, full decision history) can be 5-10MB JSON. Reading/writing blocks main thread.

**Solutions:**

1. **Async Save:**
   - Serialize on background thread using `Task.Run()`.
   - Write to disk on background thread.
   - Display "Saving..." toast on main thread. Non-blocking.

2. **Compression:**
   - GZip the JSON before writing. Reduces save file size 70-80%.
   - Negligible CPU cost on modern hardware.

3. **Lazy Load Metadata:**
   - Save slot UI loads only .meta files (tiny, <1KB each).
   - Full save file loaded only when player clicks "Load".

### 6.3 Profiling Plan

**Before Optimization:**

Profile first. Optimization without data is guesswork.

**Unity Profiler Targets:**

1. **Deep Profile a Full Campaign Playthrough:**
   - Play from Q1 to Q60 (or accelerate with time skip).
   - Identify which systems spike during quarterly ticks.
   - Check for garbage allocation spikes (causes GC stutters).

2. **UI Frame Budget:**
   - Profile the Production Pipeline Board with 3 active films.
   - Check draw call count (target: < 50).
   - Check SetPass calls (target: < 10).

3. **Save/Load:**
   - Profile a save at Q60 (largest state).
   - Measure time to serialize, time to write to disk.
   - Target: < 200ms for save, < 100ms for load.

**If Performance Misses Target:**

- **PC**: Unlikely to have issues. If so, disable particle effects, reduce UI update frequency.
- **Switch**: More constrained. May need to cap frame rate at 30fps, reduce UI animation complexity, simplify rival AI.
- **iPad**: Offload more work to background threads. Reduce canvas complexity.

---

## 7. PLATFORM CONSIDERATIONS

### 7.1 PC (Steam) — Primary Platform

**Input:**

- Mouse + Keyboard primary.
- Controller support secondary (navigate UI with D-pad/stick, confirm with A, cancel with B).

**Resolution:**

- Scalable UI from 1280×720 to 3840×2160 (4K).
- Reference resolution: 1920×1080. Scale UI Canvas with "Scale With Screen Size" mode.

**Steam Integration:**

- **Achievements:** 30-40 achievements (first film released, first Oscar win, first $500M gross, complete 2D-only campaign, etc.).
- **Cloud Save:** Via Steamworks API.
- **Rich Presence:** Display current quarter, active film count, studio name in Steam friends list.
- **Steam Input:** Use Steam Input API for controller remapping.

**Build Pipeline:**

- Unity build target: Windows x64 (primary), macOS (secondary if demand exists).
- IL2CPP backend for performance and anti-piracy (C# -> C++ compilation).

### 7.2 Nintendo Switch — Secondary Platform (Stretch Goal)

**Input:**

- Controller-first. Redesign cursor navigation for Joy-Con.
- Touchscreen in handheld mode (optional enhancement, not required).

**Performance:**

- Target 30fps. Reduce particle complexity, lower canvas rebuild frequency.
- Memory budget: 2GB max. Profile for memory leaks (Switch OS is aggressive with low-memory kills).

**Build:**

- Unity build target: Switch (requires Nintendo DevKit license and hardware).
- Test on actual hardware early — Switch emulator perf is not representative.

**Certification:**

- Nintendo lotcheck (QA certification) requires 4-6 weeks. Plan for this in schedule.
- Common lotcheck failures: crashes on suspend/resume, memory leaks, improper button prompts. Test exhaustively.

### 7.3 iPad (Stretch Goal)

**Input:**

- Touch-first. All UI elements must be finger-sized (44pt minimum tap target per Apple HIG).
- Pinch-to-zoom on production board (nice-to-have).

**Performance:**

- Target 60fps on iPad Air 4 (A14 chip).
- Metal renderer (Unity auto-selects on iOS).

**Build:**

- Unity build target: iOS.
- Requires Apple Developer account ($99/year).
- TestFlight beta testing before App Store release.

**Monetization:**

- Premium pricing ($14.99-$19.99 — no IAP, no ads).

**Certification:**

- App Review focuses on crashes, privacy, metadata accuracy.
- Include privacy manifest (required in iOS 17+). No data collection = minimal compliance.

---

## 8. BUILD PIPELINE AND TOOLS

### 8.1 Version Control

**Git + LFS:**

- Repository on GitHub (private during development).
- Git LFS for binary assets (Unity scenes, prefabs, ScriptableObjects serialized as binary, texture atlases).
- Force text serialization for scenes/prefabs/ScriptableObjects in Unity Project Settings. Enables meaningful diffs and merge conflict resolution.

**Branch Strategy:**

- `main`: Always stable, represents last known-good build.
- `dev`: Active development. Merges to `main` after weekly playtest builds pass.
- Feature branches: `feature/tech-tree-ui`, `feature/box-office-sim`, etc. Short-lived (1-2 weeks max).

**Commit Guidelines:**

- Prefix commits with system tag: `[Film] Fix DNA scoring bug`, `[UI] Production board card animation`, `[Save] Add migration for v2 format`.
- Commit often. Small commits are easier to debug than monolithic "end of day" commits.

### 8.2 Build Automation

**Unity Cloud Build (Option 1):**

- Unity's hosted CI/CD. Automatically builds on every commit to `dev`.
- Outputs Windows, macOS, Switch builds.
- Slack/Discord webhook notifications on build success/failure.

**GitHub Actions (Option 2):**

- Self-hosted CI.
- Cheaper (free for public repos, $0.008/min for private).
- More control over build environment.

**Recommended:** Start with Unity Cloud Build for simplicity. Migrate to GitHub Actions if cost or customization becomes an issue.

**Automated Build Cadence:**

- **Nightly builds** from `dev`: Full builds for Windows/Mac, uploaded to internal Dropbox/Google Drive.
- **Weekly playtest builds** from `dev`: Tagged builds shared with playtesters.
- **Release Candidate builds** from `main`: Final QA pass before Steam/Switch/iPad submission.

### 8.3 Content Tools (Unity Editor Extensions)

**Film Concept Editor:**

- Custom EditorWindow for creating FilmConceptTemplate ScriptableObjects.
- Form fields for:
  - Logline template text.
  - Variable substitution lists (Protagonist, Concept, Setting).
  - Attribute ranges (sliders for min/max).
  - Hidden risk checkboxes.
- Button: "Test Generate" — previews 5 random concepts from this template.

**Tech Tree Visualizer:**

- Custom EditorWindow showing tech tree as a node graph.
- Click node to edit in Inspector.
- Validates prerequisite chains (no circular dependencies, no orphaned nodes).
- Button: "Export Tech Tree JSON" for external balance analysis.

**Review Template Tester:**

- EditorWindow for testing review generation.
- Input: Film DNA values (8 sliders).
- Input: Projector Score (slider 0-100).
- Button: "Generate Review" — displays 10 sample reviews.
- Validates that all DNA profiles have matching templates (no gaps).

**Decision History Viewer:**

- EditorWindow (or in-game debug menu) that displays a film's full decision history as a timeline.
- For each decision: quarter, type, chosen option, DNA modifiers applied.
- Click decision to see DNA state before/after.
- Essential for debugging "why did my film score X?" questions.

### 8.4 Localization (Post-Launch)

**Initial Launch:** English only.

**Post-Launch Localization Plan:**

- Unity Localization Package for string tables.
- Externalize all UI text, film concepts, review phrases to CSV.
- Translate to: French, German, Spanish, Portuguese (Brazilian), Japanese, Simplified Chinese.
- Contract professional translators (avoid machine translation for narrative-heavy content).

**Localization Scope:**

- UI text: 5,000-8,000 words.
- Film concepts: 10,000-15,000 words (100 templates × variable options).
- Review phrases: 3,000-5,000 words.
- Total: ~25,000 words per language. Budget $0.10-$0.15/word for quality translation = $2,500-$3,750 per language.

---

## 9. TECHNICAL RISK ASSESSMENT

### 9.1 High-Risk Areas

#### Risk: Simulation Determinism Breaks

**Symptom:** Same inputs produce different outputs across sessions. Film DNA scores drift. Save/load desync.

**Cause:** Hidden non-determinism (UnityEngine.Random instead of seeded System.Random, floating-point order-of-operations variance, time-based RNG).

**Mitigation:**

- Enforce seeded RNG from day one. Code review rule: any RNG call must use `GameRNG.Next()`, not `Random.Range()`.
- Unit test critical calculations (Film DNA scoring, box office formulas) with fixed inputs. Assert exact outputs.
- Regression test suite: load a save, advance 10 quarters, save again. Diff the two saves. Should be identical (modulo RNG advancement).

**Likelihood:** Medium. Easy to introduce accidentally. Hard to debug once it spreads.

**Impact:** High. Breaks player trust ("why did my film score differently this time?"). Breaks save compatibility.

#### Risk: UI Performance Degrades on Switch

**Symptom:** Frame rate drops below 30fps when viewing production board with 3+ films.

**Cause:** Canvas rebuild cost, excessive draw calls, overdraw from layered UI elements.

**Mitigation:**

- Profile on Switch devkit early (by Month 3 of development).
- Aggressive canvas batching and static separation.
- Reduce particle effects, simplify animations.
- If perf still misses, cut Switch platform (Steam-only launch is viable).

**Likelihood:** Medium. Switch is CPU-constrained and Unity UI is not its strength.

**Impact:** Medium. Losing Switch platform reduces potential revenue but doesn't kill the game (Steam is primary).

#### Risk: Procedural Content Feels Algorithmic

**Symptom:** Film concepts and reviews feel repetitive or nonsensical. Players complain that "all films sound the same."

**Cause:** Insufficient template variety, poor variable substitution, weak authorial voice.

**Mitigation:**

- Extensive playtesting of procedural content. 30+ hour playtests to surface repetition.
- Content authoring by a writer (not a programmer). Templates need narrative craft, not code logic.
- Fallback: reduce procedural generation, increase hand-authored content. If 100 templates isn't enough, go to 200.

**Likelihood:** Medium. Procedural narrative is notoriously hard to get right.

**Impact:** High. If concepts feel generic, the greenlight decision (the game's heart) loses emotional weight.

### 9.2 Medium-Risk Areas

#### Risk: Box Office Formula Balance Is Off

**Symptom:** All films either succeed or fail predictably. No risk/reward tension.

**Cause:** Formula weights favor one strategy (e.g., SPECTACLE dominates, ORIGINALITY is worthless).

**Mitigation:**

- Spreadsheet modeling of box office formulas with 100+ simulated films.
- Playtest data collection: track every film release, DNA scores, box office results.
- Balance patch post-launch if needed (formulas are data-driven, not hardcoded).

**Likelihood:** Medium. Hard to balance before player behavior data.

**Impact:** Medium. Fixable post-launch. Not a launch-blocker unless egregious.

#### Risk: Save File Corruption

**Symptom:** Players report saves not loading, crashes on load, lost progress.

**Cause:** Save format version mismatch, incomplete save writes (disk full, crash mid-save), JSON parsing errors.

**Mitigation:**

- Write saves atomically: serialize to temp file, then rename to final save file (avoids partial writes).
- Versioned save format with migration logic.
- Extensive save/load testing in QA (save at every quarter, load at every quarter, advance, repeat).
- Backup autosaves (keep last 3) so player can revert if latest save is corrupt.

**Likelihood:** Low. Standard save/load techniques are well-proven.

**Impact:** High if it happens. Lost progress is a player trust killer.

#### Risk: Rival AI Is Too Weak or Too Strong

**Symptom:** Rivals never compete (boring) or always dominate (frustrating).

**Cause:** Rival strategy tuning, box office variance, poaching aggression.

**Mitigation:**

- Difficulty settings: Easy (rivals release fewer films, lower quality), Normal (balanced), Hard (rivals aggressive, high quality).
- Playtest with varied skill levels. Adjust rival parameters per difficulty.

**Likelihood:** Medium. AI tuning is always an iterative process.

**Impact:** Low. Tunable post-launch via data patches.

### 9.3 Low-Risk Areas

#### UI Layout and Aesthetics

**Why Low Risk:** The diegetic studio interface is a design strength but not a technical challenge. Unity's Canvas system handles this. Iteration on layout is fast.

**Worst Case:** UI doesn't look as good as mockups. Solvable with more art iteration.

#### Controller/Touchscreen Input

**Why Low Risk:** Input abstraction is Unity's strength. Mapping mouse clicks to controller buttons is straightforward.

**Worst Case:** Some UI elements are awkward with controller. Redesign those elements.

#### Integration with Steam/Switch SDKs

**Why Low Risk:** Unity plugins (Steamworks.NET, Nintendo SDK) are mature and well-documented.

**Worst Case:** Achievement integration is buggy. Ship without achievements initially, patch later.

---

## 10. DEVELOPMENT MILESTONES (TECHNICAL)

### Phase 1: Prototype (Months 1-3)

**Goal:** Prove the core loop is fun. Greenlight -> Production -> Box Office.

**Deliverables:**

- **Film Production Pipeline:**
  - FilmSimulator with all 6 phases implemented.
  - Simplified decision gates (1-2 decisions per phase, hardcoded options).
  - Film DNA scoring for all 8 attributes.
  - Decision history tracking.

- **Box Office Simulator:**
  - Full revenue calculation (opening weekend, drop-off, WOM, international).
  - Projector Score and Audience Score calculation.
  - Procedural review generation (basic phrase templates).

- **UI (Prototype Quality):**
  - Text-based UI (no diegetic studio yet — just menus and tables).
  - Greenlight Table showing film concepts.
  - Production Pipeline Board showing phase progression.
  - Box Office Results screen with reviews.

- **Save/Load:**
  - JSON serialization of StudioState.
  - Save/load buttons in main menu.

**Success Criteria:**

- Playtesters can greenlight a film, make production decisions, and understand why the film scored what it did at release.
- Core loop takes 15-20 minutes per film.
- Playtesters report feeling "creative stewardship" rather than "spreadsheet management."

**Tech Risks Addressed:**

- Simulation determinism validated (unit tests).
- Film DNA scoring is legible (post-mortem screen shows decision attribution).

### Phase 2: Vertical Slice (Months 4-6)

**Goal:** One complete campaign arc (3 films, 1995-2003) with production-quality UI and content.

**Deliverables:**

- **Diegetic Studio UI:**
  - Studio View with rooms (Greenlight Office, Production Board, Screening Room, Render Farm, Lobby).
  - Navigation between rooms (click to enter, camera transitions).
  - Corkboard aesthetic for Greenlight Table.
  - Physical production board with film cards moving through phases.

- **Talent Management:**
  - TalentManager service implemented.
  - Hiring UI (Talent Agency Board).
  - Morale and poaching systems.
  - Director/Animator assignment to films.

- **Tech Tree:**
  - Tech tree data (20 nodes: CG + 2D branches).
  - Research UI (node graph).
  - Tech effects applied to film DNA.

- **Economy:**
  - Full budget simulation (income, expenses, quarterly burn).
  - Budget UI (dashboard in studio).
  - Bankruptcy/crisis mode.

- **Procedural Content:**
  - 30 film concept templates.
  - 10 review templates.
  - Concept and review generation tested for quality.

- **Rival Studios:**
  - 2 rival studios with basic AI.
  - Rival film releases compete for box office.

**Success Criteria:**

- Playtesters complete a 3-film campaign arc in 90 minutes.
- The diegetic studio UI "feels like a place they work."
- Procedural concepts and reviews feel authored, not algorithmic.
- Budget management creates meaningful tension (not trivial, not punishing).

**Tech Risks Addressed:**

- UI performance profiled on target hardware (60fps on PC).
- Procedural content quality validated.

### Phase 3: Alpha (Months 7-10)

**Goal:** Full campaign (1995-2010, 6-10 films) with all features, content-complete.

**Deliverables:**

- **Full Campaign:**
  - Era events (2D collapse, Oscar creation, tech milestones).
  - 60-quarter timeline with pacing.
  - End-game retrospective screen.

- **All Systems Complete:**
  - Studio Soul system (hidden axis, reputation effects).
  - Sequel/franchise system.
  - Awards season (Best Animated Feature simulation).
  - Director morale showdowns, test screening decisions.

- **Content Complete:**
  - 100 film concept templates.
  - 25 review templates.
  - 40 tech tree nodes.
  - Master talent database (50+ Directors, 100+ Animators, 80+ Voice Actors).

- **Rival AI Complete:**
  - 3 rival studios with distinct strategies.
  - Poaching, competitive release timing, awards competition.

- **UI Polish:**
  - Animations (card transitions, number count-ups, particles).
  - Sound design (diegetic: render farm hum, pencil scratches, projector whir).
  - Music (era-appropriate jazz score).

**Success Criteria:**

- Full 10-hour campaign playtests complete without major bugs.
- Players report emotional investment in studio identity.
- Mid-campaign sag is mitigated (Era 3 events create tension).
- Reputation system is legible (players understand how their decisions shaped their studio).

**Tech Risks Addressed:**

- Late-game performance validated (3 simultaneous films, 50+ staff, full tech tree).
- Save/load tested at Q60 (largest state).

### Phase 4: Beta (Months 11-12)

**Goal:** QA, optimization, bug fixing. Prepare for launch.

**Deliverables:**

- **QA Pass:**
  - Full regression test suite.
  - Edge case testing (bankrupt studio recovery, all-2D campaign, sequel-only strategy).
  - Save/load stress testing.

- **Optimization:**
  - Profile-guided optimization (Unity Profiler deep dive).
  - Canvas batching, draw call reduction.
  - Amortize quarterly tick across frames.

- **Platform Builds:**
  - Windows x64 (primary).
  - macOS (if time permits).
  - Switch (if performance acceptable).

- **Steam Integration:**
  - Achievements.
  - Cloud save.
  - Rich Presence.
  - Trading cards (optional).

- **Trailer and Key Art:**
  - Gameplay trailer (2 minutes, focus on diegetic UI and decision moments).
  - Steam capsule art (studio at night, corkboard, render farm glow).

**Success Criteria:**

- Zero critical bugs (crashes, save corruption).
- Performance meets targets on all platforms.
- Steam page live, wishlist campaign begins.

**Risks Addressed:**

- All identified risks mitigated or accepted.

### Phase 5: Launch and Post-Launch (Month 13+)

**Goal:** Ship the game. Support post-launch.

**Deliverables:**

- **Launch:**
  - Steam release (Early Access or full launch, TBD).
  - Press outreach (PC Gamer, RPS, indie game sites).
  - Influencer keys (YouTube/Twitch streamers in management sim niche).

- **Post-Launch Support:**
  - Patch 1.1: Balance tweaks based on player data (box office formulas, tech tree costs).
  - Patch 1.2: Additional content (20 new film concepts, 5 new tech nodes).
  - DLC (stretch): "Streaming Wars" expansion (extends timeline to 2020, adds streaming platform competition).

**Success Criteria:**

- 10,000 units sold in first month (reasonable for indie management sim).
- "Very Positive" Steam review rating (80%+ positive).
- Community engagement (subreddit, Discord).

---

## CLOSING NOTES

This is the technical architecture for FRAMEWAR. Every system is designed to ship.

**What's proven:**

- Unity for UI-heavy sims (Two Point Hospital, Game Dev Tycoon both use Unity).
- JSON save/load for deep state (standard practice).
- Separation of simulation and presentation (testable, maintainable).
- Procedural content from authored templates (Cultist Simulator, Sunless Sea).

**What's novel:**

- Diegetic studio interface (no game has done this for film production).
- Film DNA interaction effects (HEART multiplies STORY for critics, etc.).
- Studio Soul as a hidden reputation axis.

**What's risky:**

- Procedural content quality (mitigate with extensive testing, writer-authored templates).
- UI performance on Switch (mitigate with early profiling, fallback to 30fps or cut platform).
- Simulation determinism (mitigate with strict RNG discipline, unit tests).

**Development time estimate:** 12-15 months with a team of:
- 1 programmer (you).
- 1 designer (owns system tuning, content authoring).
- 1 artist (UI art, studio environments, iconography).
- 1 audio designer (music, SFX).
- Contract QA (Month 11-12).

**Budget estimate (indie scale):** $150k-$250k (salaries + tools + marketing).

**Ship date target:** Q4 2027 (assuming greenlight in Q1 2026).

The architecture is solid. The risks are known. The game is shippable.

Now build it.

---

**End of Technical Architecture Document**

**Files Referenced in This Document:**
- /Users/burcukose/git/project-draft/games/12-framewar/pitch.md
- /Users/burcukose/git/project-draft/games/12-framewar/game-design.md
- /Users/burcukose/git/project-draft/games/12-framewar/technical-architecture.md (this document)
