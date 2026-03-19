# Voice Rules Reference

## The Voice Hierarchy (Most to Least Effective)

**Tier 1: Annotated few-shot examples.** Paste 2-3 paragraphs of your best prose with annotations explaining why each works. Format:

```
"Mei-Lin's hands found the cold stone wall before her eyes adjusted.
The dark was absolute — not the blue-gray dark of a Parisian evening
but something older, something that pressed against her face like cloth."

— Why this works: Concrete sensory detail (cold stone, pressing dark).
Short punchy sentences. Uncertainty as narrative driver. Dual-world
comparison (Paris vs. Song) through sensation, not exposition. Active
protagonist feeling her way through, not observing passively.
```

**Tier 2: Bullet-list rules with examples of each.** 10-15 rules max. Each rule with a concrete illustration:

- Past tense, deep POV, third person limited
- Show through action and body language, never label emotions
- Eliminate filter words: "she saw," "she felt," "she noticed," "she realized"
- Narration uses only vocabulary the POV character would know
- Mix sentence lengths: short for impact, medium for action, long for reflection
- Dialogue in its own paragraph; action beats over dialogue tags
- Metaphors from the character's knowledge domain (epidemiology, field medicine, Song material culture) — never from industrial, electrical, or post-19th-century imagery
- No omniscient narrator intrusions or future-knowledge hints

**Tier 3: "Write like X author" — avoid.** Produces caricature, not voice. The AI exaggerates statistical features while losing subtlety.

## The Prohibited Word List

AI-favored words that signal machine-generated prose. Add to always-on context:

```
tapestry, delve, bustling, vibrant, gossamer, labyrinthine, enigma,
symphony, crucible, realm, embark, navigate, meticulous, unleash,
harness, robust, nestled, dance (as metaphor), metamorphosis,
indelible, journey (as metaphor), daunting, palpable, myriad,
intricate, resonate, pivotal, nuanced, akin, commence, juxtapose,
multifaceted, underscore, landscape (as metaphor), tapestry (as
metaphor), fingers dancing, hum of, weight of, kaleidoscope
```

Update this list per project — add any words the AI over-produces in your specific voice.

## Deep POV Rules

Five constraints that transform generic narration into character-specific prose:

1. **No filter words.** Not "she saw the blood on the stone" but "blood on the stone, already browning at the edges."
2. **No emotion labels.** Not "she felt afraid" but "her hands wouldn't stop shaking. She pressed them flat against her thighs."
3. **POV-limited vocabulary.** Narration uses only words the character would think. An epidemiologist thinks "fecal-oral transmission," not "contamination of the water supply."
4. **Sensory priority per character.** Define what each POV character notices first (see character profiles). Load this as a one-line instruction.
5. **No information the POV character doesn't possess.** If she hasn't seen the east wing, narration can't describe it.

## Historical Fiction Voice (Period Texture Without Drift)

Three techniques that maintain register across hundreds of scenes:

**Period-appropriate source excerpts as voice samples.** Feed actual primary source material (Song dynasty letters, diaries, memoirs) rather than modern prose. This shifts the AI's baseline register without requiring explicit period language instructions.

**Register band instruction.** Include in always-on context: "Write in a style that evokes Song dynasty China through word choice and concrete period details, but remains accessible to modern readers — avoid both contemporary slang and deliberately archaic constructions."

**Period-specific metaphor domain.** Include in always-on context: "Draw metaphors from [the character's world]: canal water, silk production, seasonal agriculture, Buddhist practice, bureaucratic paperwork, market commerce, weather, disease. Never from industrial, electrical, automotive, digital, or post-19th-century imagery."
