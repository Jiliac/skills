# World Bible Reference

## Generative vs. Referential World-Building

**Generative** details shape how prose reads — load during drafting.
**Referential** details inform the author's planning — never load during drafting.

Loading referential details into AI context wastes tokens and causes exposition dumps. The AI treats loaded world-building as material that needs to be conveyed to the reader.

## Location Sensory Profiles (50-80 words each)

The highest-value world-building entries. Each recurring location gets:

```markdown
# [Location Name]

**Sounds:** [dominant ambient sounds]
**Smells:** [signature scents]
**Light:** [quality and source of illumination]
**Textures:** [underfoot, surfaces, air on skin]
**Temperature:** [ambient feel, seasonal variation]
**What's different here:** [one detail that makes this location unique]
```

Example:

```markdown
# The Canal District Market

**Sounds:** Vendor calls layered over water-slap against stone quays.
Rope creak from moored boats. A peddler's wooden clapper.
**Smells:** Fish brine, fermented grain, wet hemp rope. In summer,
the canal itself — vegetal, faintly sour.
**Light:** Filtered through canvas awnings; dappled on wet cobblestones.
**Textures:** Slick stone underfoot after rain. Rough hemp sacking.
**Temperature:** Canal breeze cuts through summer humidity.
**What's different:** The noise compresses between buildings — you
hear conversations from three stalls away.
```

## Technology / Knowledge Constraints (Always-On)

Format as "What exists / What doesn't exist." Prevents anachronisms more effectively than prohibition lists.

```markdown
# What This World Can and Cannot Do

**Communication:** News travels at horseback speed. No telegraph,
no postal system for commoners. Official courier network exists
but is state-only.
**Medicine:** Pulse diagnosis, herbal pharmacopoeia, acupuncture,
moxibustion. No germ theory, no microscopy, no surgery beyond
wound treatment. Sophisticated but axiomatically different.
**Writing:** Paper exists and is common. Printing exists (woodblock)
but books are expensive. Most records are handwritten. Ink and
brush, not pen.
**Illumination:** Oil lamps and candles. No gas, no electric light.
Night is genuinely dark.
**Food:** No chili peppers, no corn, no potatoes, no tomatoes,
no peanuts (all New World). Rice, wheat, millet, pork, fish,
soy, tea, rice wine.
```

## Social Norms / Forms of Address (Per-Scene)

Load when drafting dialogue scenes. Keep to 100-150 words covering the norms active in the current scene's social context.

```markdown
# Social Norms: Merchant-Official Interaction

**Address:** Officials addressed as "daren" (大人). Merchants
bow but do not kneel. Self-deprecation is required when speaking
up to officials.
**Gender:** Women of merchant households manage inner economy but
do not appear in official transactions. A woman addressing an
official directly is a serious breach.
**Hierarchy signals:** Who sits, who stands. Who speaks first.
Who pours tea for whom. These are not decorative — they are
power declarations.
**Dangerous topics:** Criticizing reform policies, mentioning
factional purges, questioning tax assessments.
```

## What Never Gets Loaded

- Full political hierarchies (distill into scene-relevant constraints: "magistrates can impose curfew without appeal")
- Comprehensive genealogies and family trees
- Historical timelines beyond the current book's scope
- Maps and spatial layouts (inform beat sheets instead)
- Magic/technology system mechanics beyond what constrains the current scene
- Research notes and source citations

These inform the beat sheets written during scene-architect planning. The beat sheet is what gets loaded — not the raw world-building behind it.

## The "Setting as Character" Approach

Major locations that appear in 5+ scenes deserve the same care as character profiles. Track how the location changes over time:

```markdown
# The Clinic (evolving)

**Book 1, early:** Empty room. Dirt floor. One table. Smells of
dust and old incense from the previous tenant.
**Book 1, mid:** Swept. Herb bundles hanging from rafters. A proper
examination table. Smells of boiled water and dried chrysanthemum.
**Book 1, late:** Crowded. Patients on mats along the walls. The
smell has changed — carbolic (her improvised disinfectant), sweat,
and something sweet-metallic she tries not to name.
```
