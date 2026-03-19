# Character Profile Reference

## Protagonist Profile Template (~200-300 words total)

```markdown
# [Character Name]

## Core (25-30 words)

Age, role, fatal flaw, conscious want, unconscious need. Dramatic
tensions, not personality adjectives. "Pride masks deep insecurity"
outperforms "proud and insecure."

## Speech Patterns (50-80 words)

Three non-negotiable traits:

1. **Lexical habit:** vocabulary choice under stress
2. **Syntactic pattern:** how sentence structure changes with emotion
3. **Pragmatic tell:** physical behavior revealing inner state

Example: "Clinical vocabulary when calm — 'fecal-oral transmission,'
'case fatality rate.' Contractions increase with emotion. Under stress,
reverts to French micro-expressions (shrugs, lip purse) before catching
herself. Uses rhetorical questions as deflection."

## Arc Trajectory (30-40 words)

Opens / Midpoint / Closes structure.
"Opens: competent loner, trusts systems over people.
Midpoint: forced to rely on people she can't control.
Closes: learns that institutions ARE people."

## Sensory Priority (20-30 words)

What does this character notice first? Defines deep POV narration.
"Notices: sanitation infrastructure, water sources, crowd density,
disease indicators, food handling. Ignores: architecture, politics,
aesthetics — unless they connect to health."

## Voice Sample (200-300 words)

Write 2-3 paragraphs of exemplary prose in this character's POV voice.
Load alongside character card during drafting sessions.
```

## Supporting Cast Template (~100-150 words)

```markdown
# [Character Name]

**Relationship to POV:** [one sentence]
**Speech pattern:** [one defining trait]
**Behavioral tell:** [one physical habit revealing inner state]
**Arc in this book:** [one sentence: opens → closes]
**Relationship line:** "[POV character] → [this character]: [tension]"
```

No physical descriptions in AI-visible context. Physical traits cause the AI to over-mention eye color, hair, and build — producing prose that reads like a police report. Keep physical descriptions in author-reference notes.

## Relationship Mapping

Most token-efficient format: one sentence per relationship pair, stored in the relevant character's profile.

```
Mei-Lin → Dr. Chen: grudging respect; he dismisses her methods
but relies on her results. She resents needing his institutional cover.

Mei-Lin → Widow Luo: first real ally; Luo provides social cover
and local knowledge in exchange for medical help for her household.
```

Load relationship lines only when both characters appear in the current scene.

## Character Arc Tracking (Series)

Per book, add a 50-100 word progression entry to each major character's file:

```markdown
## Book 2 Progression

- Emotional state at book open: [one line]
- Key relationship changes: [one line per change]
- Knowledge/skills gained: [one line]
- Emotional state at book close: [one line]
- Unresolved tension carried to Book 3: [one line]
```

These progression entries override earlier baseline descriptions when loaded. Without them, the AI defaults to Book 1 emotional states — the "reset effect."
