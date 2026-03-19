---
name: novel-bible
description: Build and maintain a structured novel bible (character profiles, world entries, voice rules, continuity tracking) optimized for AI-assisted scene drafting. Use when starting a new book or series, when prose output lacks voice consistency or character distinctiveness, when continuity errors appear across scenes, or when you need to define what context gets loaded during drafting sessions.
---

# Novel Bible

Build a three-layer context system for AI-assisted fiction drafting: always-on voice rules, selectively loaded character/world entries, and per-scene continuity state.

## When to Use

- Starting a new book or series — build the bible before drafting
- Prose output sounds generic or loses character voice — voice rules need tightening
- Continuity errors between scenes — tracking system needs setup
- Unsure what context to load during a drafting session — loading strategy needed
- Beginning a new book in an existing series — series-level bible needs updating

## What This Skill Does NOT Do

- Story architecture (use `builder-arc-planner` or `harris-thriller-planner`)
- Scene-level planning (use `scene-architect`)
- Prose drafting or revision (use drafting/revision skills)
- Historical research (use `historical-fiction-research`)

## The Three-Layer Architecture

### Layer 1: Always-On (~800-1,500 words)

Loaded in system prompt for every drafting session. Never changes mid-session.

- **Voice rules** with annotated examples (300-500 words)
- **POV/tense/distance rules** (100-150 words)
- **Prohibited word list** (50-100 words)
- **Technology/knowledge constraints** — what exists, what doesn't (150-200 words)
- **Series premise + overarching arc** (200-300 words, series only)

### Layer 2: Per-Scene Selective (~800-1,500 words)

Loaded based on which characters, locations, and threads appear in the current scene.

- **Character profiles** — protagonist (200-300 words + internal arc block), supporting cast (100-150 words each)
- **Character web table** (load when multiple thematically significant characters share a scene)
- **Location sensory profiles** (50-80 words each)
- **Social norms / forms of address** relevant to scene (100-150 words)
- **"Previously on" summaries** of recent chapters (150-300 words each)
- **Character arc progression** for current book (50-100 words per character)

### Layer 3: Author-Reference Only (never loaded during drafting)

Informs beat sheets and scene planning, but kept out of AI context.

- Full political hierarchies and institutional structures
- Comprehensive genealogies and maps
- Historical research files and timelines
- Brainstorming notes, cut scenes, revision history
- Unresolved thread register (informs beat sheets instead)

## Process: Building the Bible

### Step 1: Voice Rules

Write 2-3 annotated passages of your best prose. For each, note WHY it works. Add bullet-list rules and a prohibited word list. See `references/voice-rules.md`.

### Step 2: Character Profiles

For each character, write: core tension (25-30 words), speech patterns with 3 specific traits (50-80 words), arc trajectory (30-40 words), sensory priority (20-30 words). Add a 200-300 word voice sample for POV characters. See `references/character-profiles.md`.

For the **protagonist**, also complete the internal arc block:

```
GHOST: [Backstory event causing present weakness]
LIE: [False belief the protagonist operates under — one sentence]
PSYCHOLOGICAL WEAKNESS: [How the flaw hurts the protagonist themselves]
MORAL WEAKNESS: [How the flaw hurts others]
PSYCHOLOGICAL NEED: [What must change internally]
MORAL NEED: [What must change in how they treat others]
DESIRE: [External goal in this story]
SELF-REVELATION: [What the protagonist learns — or fails to learn]
ARC TYPE: Positive / Negative-Fall / Negative-Corruption / Tragic (revelation too late)
```

This block bridges the `harris-thriller-planner`'s desire/need definition (Phase 5) with the bible's character profiles. Desire should match the planner's statement; the need fields inform behavioral tells, speech patterns, and arc trajectory already tracked in the profile.

### Step 2b: Character Web

After writing individual profiles, build a **character web table** mapping how every thematically significant character relates to the protagonist's central moral problem. This is not a relationship map (who knows whom) — it is a thematic comparison system (how each character embodies a different answer to the same moral question).

**Character Web Table** (include 5-8 characters with thematic weight):

| Character | Story Function                                        | Weakness          | Desire (in this story) | Approach to Central Moral Problem    |
| --------- | ----------------------------------------------------- | ----------------- | ---------------------- | ------------------------------------ |
| [Name]    | Hero / Opponent / Ally / Fake-Ally Opponent / Subplot | [Behavioral flaw] | [What they want]       | [Their answer to the moral question] |

**Include** characters who participate in the central moral conflict. **Exclude** purely functional characters (a clerk who appears in two scenes to stamp a tally) — they stay in the profiles but don't enter the web.

**Test:** If a character in the web has no clear approach to the moral problem, they may be functional rather than thematic. Either find their thematic connection or remove them from the web (they can still appear in the story).

**Four-Corner Opposition** (optional but recommended for complex stories):

Place 4 core characters at the corners of a square — each representing a fundamentally different approach to the central moral problem. The 6 lines between them (each corner vs. every other) generate the story's moral complexity. Truby's principle: "Your moral argument will always be simplistic if you use a two-part opposition."

{{ NOTE: The research proposed Zhao Yu / Betrayer / Guild headman / Resentful merchant for the four corners. This feels forced — the headman and resentful merchant are misdirection devices in the plot, not genuine thematic opponents. The stronger four-corner may be Zhao Yu / Father / Betrayer / Partner: four different answers to "what do you sacrifice for ambition?" Decide when applying to the specific project. }}

### Step 3: World Entries

For each recurring location, write a 50-80 word sensory profile (sounds, smells, light, textures, temperature). Write technology/knowledge constraints and social norms. See `references/world-bible.md`.

### Step 4: Continuity System

Set up rolling chapter summaries (150-300 words each) and character state tracking. For series work, add per-book summaries and cross-book evolution entries. See `references/continuity-tracking.md`.

### Step 5: Context Loading Plan

Classify every bible entry as always-on, per-scene, or author-reference. Test total token budget. See `references/context-loading.md`.

## Output Format

Deliver bible as separate markdown files per layer:

- `voice-rules.md` (Layer 1)
- `characters/[name].md` (Layer 2, one file per character)
- `character-web.md` (Layer 2 — character web table + four-corner opposition)
- `locations/[name].md` (Layer 2, one file per location)
- `world-constraints.md` (Layer 1)
- `continuity/book-[N]-summary.md` (Layer 2, rolling)
- `series-bible.md` (Layer 1, series only)

## References

- `references/voice-rules.md` — Annotated example format, prohibited words, historical fiction voice
- `references/character-profiles.md` — Profile template, speech patterns, voice samples
- `references/world-bible.md` — Location profiles, technology constraints, generative vs. referential
- `references/continuity-tracking.md` — Chapter summaries, state tracking, series continuity
- `references/context-loading.md` — Token budgets, loading strategy, context pollution avoidance
