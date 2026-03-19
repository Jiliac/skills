# Context Loading Strategy

## Token Budget for a Scene Drafting Session

| Component                       | Allocation | Words       |
| ------------------------------- | ---------- | ----------- |
| System prompt / voice rules     | 2-5%       | 200-600     |
| Active character profiles       | 5-10%      | 500-1,200   |
| World/setting entries           | 3-5%       | 300-600     |
| Scene beat sheet                | 3-5%       | 300-600     |
| "Previously on" summaries       | 5-15%      | 500-2,000   |
| Recent prose (1-3 prior scenes) | 20-30%     | 2,000-4,000 |
| Output reservation              | 10-15%     | 1,000-2,000 |

Keep active context below 50% of window capacity. The "lost in the middle" effect: models lose tokens in the middle of context. Place critical instructions at the very beginning (system prompt) and very end (current scene instructions).

## What Gets Loaded When

**Every scene (always-on):**

- Voice rules + annotated examples
- POV/tense/distance rules
- Prohibited word list
- Technology/knowledge constraints
- Series premise (series only)

**Per-scene (selective):**

- Character profiles for characters IN this scene only
- Location sensory profile for this scene's setting
- Social norms relevant to this scene's context
- Chapter summaries of prior chapters
- Full text of 1-3 most recent scenes
- Character arc progressions (current book)
- Scene beat sheet from scene-architect

**Never during drafting (author-reference):**

- Full political hierarchies
- Genealogies, maps, comprehensive timelines
- Research files and source notes
- Brainstorming, cut scenes, revision history
- Unresolved thread register
- Earlier versions of voice rules or profiles

## Context Pollution: What Degrades Output

**Overstuffed character descriptions.** Abstract personality adjectives ("brave, compassionate") consume tokens while producing generic prose. Physical descriptions cause the AI to mention eye color in every scene.

**Full manuscript dumps.** Even when they fit technically, performance drops measurably above 60K-120K tokens. Signal-to-noise ratio collapses.

**Revision history in context.** Every iterative refinement, abandoned direction, and tangential discussion accumulates as noise.

**Conflicting instructions.** Outdated voice rules or character profiles create incoherent output as the model tries to satisfy contradictory requirements.

**Over-detailed world-building.** Full political hierarchies cause the AI to exposition-dump. Distill into scene-relevant constraints.

## The Anti-Drift Instruction

Include in scene-level instructions when drafting:

"All paragraphs should take place during the timeframe of the current scene beats. Focus on fully developing the given story beats rather than rushing to new plot points or adding events beyond this scene."

This prevents the AI from advancing the plot past the beat sheet boundaries.

## Scene Drafting Session Setup

1. Load always-on context (voice rules, constraints, series premise)
2. Load per-scene context (characters present, location, recent summaries)
3. Load scene beat sheet from scene-architect
4. Load full text of the previous scene for tonal continuity
5. Draft in 1,000-2,000 word passes
6. After each pass, review before continuing to next scene
