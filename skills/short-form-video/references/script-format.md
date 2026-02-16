# The 6-Column Annotated Script Format

Production-ready scripts use a 6-column format expanded from traditional broadcast AV scripts. Every frame is intentional. Every second is directed.

## Header Block

Every script starts with:

```
Title: [video title]
Platform: [TikTok / YouTube Shorts / Instagram Reels / Cross-post]
Framework: [HTP / PAS / Myth-Truth-Proof / etc.]
Duration: [Xs]
Style: [Talking head / Faceless / Tutorial / Story / Hybrid]
Aspect Ratio: 9:16
```

## The 6 Columns

| Column           | What it contains                         | Convention                                                           |
| ---------------- | ---------------------------------------- | -------------------------------------------------------------------- |
| **TIME**         | Running timecode                         | `0:00–0:03` format                                                   |
| **VISUAL**       | Shot type, camera direction, B-roll      | Directions in ALL CAPS                                               |
| **VOICEOVER**    | Spoken words                             | `(V.O.)` for voiceover, `(OC)` for on-camera. Emphasis words in CAPS |
| **TEXT OVERLAY** | Exact text, position, animation, timing  | Text in quotes, position in brackets                                 |
| **AUDIO/SFX**    | Music mood cues, sound effects           | ALL CAPS for SFX                                                     |
| **EDIT NOTES**   | Transitions, speed ramps, platform notes | Freeform                                                             |

## Visual Direction Vocabulary

**Shot sizes** (closest → widest):

- ECU — extreme close-up (detail shots: hands, screen, product)
- CU — close-up (standard talking head, face fills frame)
- MCU — medium close-up (chest up)
- MS — medium shot (waist up)
- WS — wide shot (full body or environment)

**Camera movements**:

- PAN L/R — rotate camera left/right
- TILT UP/DOWN
- ZOOM IN/OUT
- PUSH IN — slow dolly toward subject (emphasis)
- PULL BACK — reveal

**Short-form edit terms**:

- JUMP CUT — abrupt cut within same angle (removes pauses)
- PUNCH IN — post-production zoom simulating a cut
- SPEED RAMP — normal to slow-mo transition
- SNAP ZOOM — quick abrupt zoom for emphasis
- B-ROLL: [description] — cutaway footage

## Text Overlay Annotation

Five properties per overlay:

1. **Content**: exact text in quotes
2. **Position**: `[CENTER]`, `[LOWER THIRD]` / `[L3]`, `[UPPER]`
3. **Animation**: `(POP)`, `(FADE)`, `(TYPEWRITER)`, `(SLIDE L/R)`, `(SHAKE)`
4. **Font emphasis**: `[BOLD]`, `[COLOR: RED]`, `[SIZE: LG]`
5. **Timing**: `IN @ 0:03`, `HOLD 2s`, `OUT @ 0:06`, or `SYNC W/ VO`

Example: `"Stop sending cold emails" [CENTER] (POP) [BOLD, COLOR: WHITE, SIZE: LG] IN @ 0:01 — HOLD 3s`

## Audio Annotation

**Music flow**: MUSIC IN / MUSIC UNDER / MUSIC UP / MUSIC OUT
**Mood cues**: `MUSIC: TENSE LO-FI, UNDER` or `MUSIC: UPBEAT ELECTRONIC`
**Sound effects**: `SFX:` prefix — `SFX: WHOOSH`, `SFX: DING`, `SFX: BASS DROP`

Common short-form SFX: WHOOSH, POP, DING, CLICK, BASS DROP, NOTIFICATION PING, DRAMATIC HIT, ERROR BUZZ, CASH REGISTER, RECORD SCRATCH.

Music sits **-5 to -25 dB** below voice. Silence ≠ no audio.

## Transition Notation

- CUT TO: (standard, often implied)
- JUMP CUT: (within same subject)
- SMASH CUT TO: (jarring emphasis)
- WHIP TO: (fast pan blur)
- ZOOM TRANSITION:
- GLITCH TRANSITION:
- SNAP TRANSITION: (synced to beat drop)

## Production Style Adjustments

**Talking head**: VOICEOVER column dominates. Add delivery cues: `[LEAN IN, lower voice]`, `[HIGH ENERGY]`, `[PAUSE for emphasis]`. Mark B-roll cutaway moments.

**Faceless/voiceover**: VISUAL column dominates (60–70% of script attention). Stock footage must be specific: "OVERHEAD shot of laptop on desk with coffee," not "show laptop." Specify B-roll pacing per clip.

**Tutorial/screen share**: Use `[CURSOR]`, `[ZOOM: 200%]`, `[HIGHLIGHT: Yellow box]`, `[ARROW: step 1 → step 2]`. Jump cuts between steps. Mark pauses: `[PAUSE 1s — let viewer see result]`.

**Hybrid**: Mark transitions explicitly: `[CUT TO B-ROLL: montage of ...]`, `[RETURN TO TALKING HEAD]`, `[FULL SCREEN GRAPHIC: stat card]`. B-roll covers 40–60% of video.

## Complete Example: PAS Framework, 30 Seconds, Hybrid Style

```
Title: Why Your Cold Emails Get Ignored
Platform: Cross-post
Framework: PAS
Duration: 30s
Style: Hybrid (talking head + B-roll)
Aspect Ratio: 9:16
```

| TIME      | VISUAL                                                          | VOICEOVER                                                                                             | TEXT OVERLAY                                                                                                       | AUDIO/SFX                                             | EDIT NOTES                                             |
| --------- | --------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------- | ------------------------------------------------------ |
| 0:00–0:03 | MCU TALKING HEAD — OC, leaning in, urgent expression            | "Your cold emails are getting ignored — and it's not because of your offer."                          | **"Your cold emails are getting IGNORED"** [CENTER] (POP) [BOLD "IGNORED", COLOR: RED] IN @ 0:00 HOLD 3s           | SFX: NOTIFICATION PING / MUSIC IN: TENSE LO-FI, UNDER | JUMP CUT into frame. Hook in 1.5s. Captions burned in. |
| 0:03–0:07 | CUT TO: B-ROLL — CU laptop screen, unread inbox. SLOW PAN.      | (V.O.) "Most cold emails start with 'Hi, my name is' and talk about the sender for three paragraphs." | **"Hi, my name is..."** [CENTER] (TYPEWRITER) [ITALIC, GRAY] IN @ 0:03 OUT @ 0:06                                  | SFX: TYPING CLICKS, soft                              | B-roll: unread emails. Color grade: cool/desaturated.  |
| 0:07–0:12 | SMASH CUT TO: MCU TALKING HEAD — OC, frustrated gesture         | "Nobody cares. They saw zero relevance and deleted it in two seconds."                                | **"Zero relevance = DELETE"** [CENTER] (SHAKE) [BOLD, RED] IN @ 0:09 HOLD 3s                                       | SFX: ERROR BUZZ / MUSIC: TENSION BUILDS               | PUNCH IN on "Nobody cares." JUMP CUTS between phrases. |
| 0:12–0:17 | CUT TO: B-ROLL — OVERHEAD phone, finger swiping/deleting emails | (V.O.) "They get 50 of these a day. Yours looks exactly like the other 49."                           | **"50 emails/day"** [UPPER] (SLIDE L) → **"Yours = #50"** [CENTER] (POP) [YELLOW] IN @ 0:14                        | SFX: WHOOSH per swipe                                 | Speed ramp swiping to 1.5×. AGITATION beat.            |
| 0:17–0:25 | SMASH CUT TO: MS TALKING HEAD — OC, calm confidence             | "Here's the fix. First line: their pain point. Second line: proof you solve it. That's it."           | **"Lead with THEIR problem"** [CENTER] (POP) IN @ 0:17 → **"1. Pain point"** → **"2. Proof"** (SLIDE R, staggered) | SFX: DING at "fix" / MUSIC: SHIFTS UPBEAT             | Widen to MS for contrast. Music pivot = SOLUTION.      |
| 0:25–0:30 | CU TALKING HEAD — OC, direct eye contact, nod                   | "Your email is a mirror, not a megaphone. Save this."                                                 | **"Mirror, not megaphone"** [CENTER] (POP) IN @ 0:25 → **"SAVE"** [L3] (FADE) IN @ 0:28                            | MUSIC OUT / SFX: SPARKLE                              | FREEZE FRAME 0.5s. Loop-friendly ending.               |

**Caption:** Most cold emails fail in the first line. Not because of the offer — because of the angle. Lead with their problem, not your pitch. (Save for your next outreach campaign)

**Hashtags:** #coldemail #salesstrategy #b2bsales #outreach

**Word count:** 78 words | **Reading level:** 4th grade | **Pattern interrupts:** 6 across 30s (one every ~5s)

## Word Count Guidelines

| Duration | Voiceover words | Educational pace |
| -------- | --------------- | ---------------- |
| 15s      | ~35–40 words    | 130–150 WPM      |
| 30s      | ~70–80 words    | 140–160 WPM      |
| 45s      | ~100–115 words  | 140–160 WPM      |
| 60s      | ~140–160 words  | 140–170 WPM      |
| 90s      | ~200–230 words  | 140–160 WPM      |

For new/complex concepts: slow to 120–130 WPM. TikTok native pace: 170–200 WPM.
