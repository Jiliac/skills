# Visual Style Baseline

Defaults so multiple artifacts in a session feel like they came from the same hand.

## Typography

- **Font stack — sans:** `ui-sans-serif, system-ui, -apple-system, "Segoe UI", Inter, Roboto, "Helvetica Neue", Arial, sans-serif`
- **Font stack — mono:** `ui-monospace, SFMono-Regular, "JetBrains Mono", Menlo, Monaco, Consolas, monospace`
- **Base size:** 15px, line-height 1.55
- **Scale:** body 15 / small 13 / h3 16 (uppercase, letter-spaced) / h2 20 / h1 28 / display 48
- **Tracking:** `-0.01em` on h1 and display only
- **Numerals:** `font-variant-numeric: tabular-nums` for any column of numbers (timelines, tables, diff line numbers)

## Color

Dark by default, light via `prefers-color-scheme`. Keep palettes small.

| Token       | Dark      | Light     | Use                                        |
| ----------- | --------- | --------- | ------------------------------------------ |
| `--bg`      | `#0b0c0f` | `#fafafa` | page background                            |
| `--panel`   | `#13151b` | `#ffffff` | cards, code blocks                         |
| `--ink`     | `#e8eaee` | `#15161a` | primary text                               |
| `--ink-dim` | `#9aa0aa` | `#5c606a` | secondary text                             |
| `--line`    | `#23262e` | `#e6e7eb` | borders, dividers                          |
| `--accent`  | `#7c9cff` | `#3b5bdb` | links, highlights, recommended card border |
| `--good`    | `#4ade80` | `#16a34a` | success tags, +diff                        |
| `--warn`    | `#fbbf24` | `#d97706` | caution tags                               |
| `--bad`     | `#f87171` | `#dc2626` | error tags, -diff                          |

Never colour-only. Pair color with text or icon: `class="tag tag-warn">Behavior change`.

## Spacing

Single 8-step scale. Use only these values.

`4 · 8 · 12 · 16 · 24 · 32 · 48 · 64`

Mapped to `--s-1` through `--s-8`. Don't introduce 6, 10, 14, 20.

## Radii

`6 · 10 · 16` for small / medium / large. Pills get `999px`.

## Borders

`1px solid var(--line)` is the only border style. Never `2px`, never dashed. Use stronger color for emphasis (`var(--accent)`).

## Shadows

Avoid by default. If needed: `0 1px 2px rgba(0,0,0,0.2)` on dark, `0 1px 2px rgba(15,17,21,0.05)` on light. No multi-layer "elevation" shadows.

## Motion

- **Durations:** 150ms (micro, hover), 240ms (default), 400ms (substantial)
- **Easing:** `cubic-bezier(0.2, 0.8, 0.2, 1)` for entrances; `ease-in-out` for state toggles; never `linear` except for progress bars
- **`prefers-reduced-motion`:** respect it — wrap any animation in `@media (prefers-reduced-motion: no-preference) { … }` and provide an instant fallback

## Iconography

If icons are needed, use Lucide via CDN: `<script src="https://unpkg.com/lucide@latest"></script>` then `<i data-lucide="check"></i>` and `lucide.createIcons()`. Otherwise use inline SVG. Avoid emoji as UI affordances — fine in body copy only when the user has explicitly used them.

## Layout

- Main column `max-width: 980px`, centred, `padding: 32px 24px`
- Cards: `.panel` class — `var(--panel)` bg, `1px solid var(--line)`, `10px` radius, `16px` padding
- Grids: `display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 16px`
- Mobile breakpoint: 720px, collapse all multi-column grids to single column

## Accessibility floor

- Focus visible on every interactive element (`:focus-visible { outline: 2px solid var(--accent); outline-offset: 2px; }`)
- Contrast ratio ≥ 4.5:1 for body text in both themes (the palette above clears this)
- `<dialog>` over custom modals — it gives Escape-to-close and focus trapping for free
- Every `<img>` has `alt`; every standalone icon has `aria-label` or is `aria-hidden="true"` if decorative
- Skip-to-content link if the page has nav

## Voice

Artifact copy is terse, declarative, present tense. No "we", no "you" (except in checklists or instructions to the reader). Cut adjectives. The visuals carry the warmth — the words carry the facts.
