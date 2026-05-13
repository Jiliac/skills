---
name: html-artifacts
description: Produce single-file HTML artifacts instead of markdown when the medium matters — side-by-side option comparisons, annotated diffs, module/architecture maps, animation sandboxes, design-token swatches, drag-and-drop boards, post-mortem timelines, clickable flows, and any "document you'd actually read" instead of skim. Use when about to produce a long markdown response whose content has visual, spatial, or interactive shape. Source: https://thariqs.github.io/html-effectiveness
---

# HTML Artifacts

Produce a self-contained `.html` file when content has shape — comparisons, motion, spatial layout, or interaction — instead of flattening it into linear markdown.

The core claim: each HTML artifact trades a document the user would skim for one they would actually read.

## When to use

Before writing a long markdown response, ask:

- Am I presenting multiple options to be compared?
- Am I describing motion, easing, transitions, or interaction?
- Am I describing spatial relationships (diffs, call graphs, module maps, architectures)?
- Am I producing a recurring structured document (post-mortem, PR review, design proposal)?
- Am I showing design tokens, component variants, or palettes?
- Would the user benefit from clicking, dragging, or toggling instead of reading?

If yes to any, produce an HTML artifact. Otherwise markdown is fine.

**Default heuristic:** if more than three paragraphs describe layout, visual, or interactive content, switch to HTML.

## When NOT to use

Markdown still wins for:

- Short answers, code review feedback in chat, single code snippets
- Files that must be committed and read in a terminal/editor (READMEs, ADRs, plain specs)
- Anything the user explicitly asks for as markdown or plain text
- Production UI or frontend code → use `frontend-design`
- Slide presentations → use `frontend-slides`

## Architecture rules

Every artifact MUST be:

1. **A single `.html` file** — no separate CSS, JS, or asset files
2. **Self-contained** — opens by double-click or `open file.html`, no server required
3. **Build-free** — no npm, no bundler, no preprocessor, no JSX
4. **Network-light** — inline CSS and JS; CDN only when essential (e.g., a charting lib)
5. **Exportable** — if the artifact accepts state changes, include a visible Export or Copy button that emits the result as text the user can paste back into chat, a PR, or a commit

See `references/architecture.md` for the scaffold.

## Pattern catalogue

Pick the pattern that matches the content's shape. Full recipes in `references/patterns.md`.

| Content shape                      | Pattern                                                      |
| ---------------------------------- | ------------------------------------------------------------ |
| Multiple options to weigh          | Side-by-side cards with trade-offs inline                    |
| Code-change review                 | Annotated diff with margin notes + severity tags             |
| Module / architecture / call graph | Boxed-and-arrowed map (inline SVG)                           |
| Design system                      | Token swatches + component contact sheet                     |
| Animation / transition             | Sandbox with adjustable duration and easing                  |
| Multi-screen flow                  | Clickable flow linking screens                               |
| Long-form doc                      | Collapsible sections, tabbed code, hover glossary, TL;DR box |
| Incident review                    | Post-mortem with minute-by-minute timeline + log excerpts    |
| Plan / proposal                    | Timeline with data-flow diagrams, milestones, risk callouts  |
| Stateful triage                    | Drag-and-drop board with Export button                       |

## Workflow

1. **Decide.** Apply the "When to use" heuristic. If markdown wins, stop.
2. **Scaffold.** Start from the boilerplate in `references/architecture.md`.
3. **Style.** Apply the baseline in `references/visual-style.md` so artifacts in the same session feel consistent.
4. **Compose.** Drop in the pattern(s) from `references/patterns.md` that fit the content.
5. **Save.** Write to a sensible path (a `/tmp/<slug>-<YYYY-MM-DD>.html` or a project `tmp/` directory) and tell the user the absolute path.
6. **Hand off.** Do not re-summarise the artifact's content in chat. The artifact IS the message.

## Feedback loop

HTML artifacts close a tighter loop than markdown:

- Generate → user opens → reacts to concrete visuals → gives concrete feedback
- Regenerate or patch the file in place; never describe changes only in prose
- For stateful UIs: user manipulates → clicks Export → pastes result back

Treat the file as the artifact. The agent's job is to keep it accurate as the conversation evolves.

## Checklist

Before handing the artifact to the user:

- [ ] Single `.html` file, opens with no server
- [ ] No external assets required (or only well-known CDNs, and you said so)
- [ ] Renders in both dark and light mode via `prefers-color-scheme`
- [ ] Keyboard navigable: visible focus rings, sensible Tab order, Escape closes dialogs
- [ ] Mobile-readable: collapses to single column below ~720px
- [ ] If interactive: has an Export, Copy, or Download button
- [ ] Saved to a sensible path; path communicated to user

## References

- `references/architecture.md` — single-file scaffold, font stack, dark mode, no-build philosophy
- `references/patterns.md` — concrete HTML/CSS recipes for each pattern in the table above
- `references/visual-style.md` — typography, color, spacing, motion defaults so artifacts feel consistent
