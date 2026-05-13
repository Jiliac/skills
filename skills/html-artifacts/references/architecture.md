# Architecture

Rules and scaffold for single-file HTML artifacts.

**Contents**

- Hard rules
- Scaffold (HTML5 boilerplate with inline tokens + dark/light mode)
- File naming and location
- Export button pattern
- What to avoid

## Hard rules

- **One file.** All CSS in a `<style>` block, all JS in a `<script>` block at the end of `<body>`.
- **No build.** No JSX, no TypeScript, no ES modules with external imports, no SCSS. Plain HTML, plain CSS, plain JS.
- **No fetch on load** unless the artifact's purpose explicitly requires fresh data (rare). Bake data into the page as a JSON `<script type="application/json" id="data">…</script>` block and parse it.
- **CDN allowed only for** charting (`d3`, `chart.js`), syntax highlighting (`highlight.js`, `prism`), or icons (`lucide`), and only when the artifact's pattern genuinely needs them. Otherwise inline.
- **No fonts from Google Fonts** unless typography is the point of the artifact. Use the system-font stack.

## Scaffold

Start every artifact from this boilerplate:

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width,initial-scale=1" />
    <title>TITLE</title>
    <style>
      :root {
        --bg: #0b0c0f;
        --panel: #13151b;
        --ink: #e8eaee;
        --ink-dim: #9aa0aa;
        --line: #23262e;
        --accent: #7c9cff;
        --good: #4ade80;
        --warn: #fbbf24;
        --bad: #f87171;
        --r-sm: 6px;
        --r-md: 10px;
        --r-lg: 16px;
        --s-1: 4px;
        --s-2: 8px;
        --s-3: 12px;
        --s-4: 16px;
        --s-5: 24px;
        --s-6: 32px;
        --s-7: 48px;
        --s-8: 64px;
        --font-sans:
          ui-sans-serif, system-ui, -apple-system, "Segoe UI", Inter, Roboto,
          "Helvetica Neue", Arial, sans-serif;
        --font-mono:
          ui-monospace, SFMono-Regular, "JetBrains Mono", Menlo, Monaco,
          Consolas, monospace;
      }
      @media (prefers-color-scheme: light) {
        :root {
          --bg: #fafafa;
          --panel: #fff;
          --ink: #15161a;
          --ink-dim: #5c606a;
          --line: #e6e7eb;
          --accent: #3b5bdb;
        }
      }
      * {
        box-sizing: border-box;
      }
      html,
      body {
        margin: 0;
        padding: 0;
      }
      body {
        background: var(--bg);
        color: var(--ink);
        font-family: var(--font-sans);
        font-size: 15px;
        line-height: 1.55;
        -webkit-font-smoothing: antialiased;
      }
      main {
        max-width: 980px;
        margin: 0 auto;
        padding: var(--s-6) var(--s-5);
      }
      h1,
      h2,
      h3 {
        line-height: 1.25;
        margin: 0 0 var(--s-3);
      }
      h1 {
        font-size: 28px;
        letter-spacing: -0.01em;
      }
      h2 {
        font-size: 20px;
        margin-top: var(--s-6);
      }
      h3 {
        font-size: 16px;
        margin-top: var(--s-5);
        color: var(--ink-dim);
        text-transform: uppercase;
        letter-spacing: 0.06em;
      }
      p {
        margin: 0 0 var(--s-3);
        color: var(--ink);
      }
      code,
      pre {
        font-family: var(--font-mono);
        font-size: 13px;
      }
      pre {
        background: var(--panel);
        padding: var(--s-3) var(--s-4);
        border-radius: var(--r-md);
        border: 1px solid var(--line);
        overflow: auto;
      }
      a {
        color: var(--accent);
        text-decoration: none;
      }
      a:hover {
        text-decoration: underline;
      }
      button {
        font: inherit;
        cursor: pointer;
      }
      :focus-visible {
        outline: 2px solid var(--accent);
        outline-offset: 2px;
        border-radius: 4px;
      }
      .panel {
        background: var(--panel);
        border: 1px solid var(--line);
        border-radius: var(--r-md);
        padding: var(--s-4);
      }
      .row {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
        gap: var(--s-4);
      }
      .muted {
        color: var(--ink-dim);
      }
      .tag {
        display: inline-block;
        padding: 2px 8px;
        border-radius: 999px;
        font-size: 12px;
        border: 1px solid var(--line);
      }
      .tag-good {
        color: var(--good);
        border-color: color-mix(in srgb, var(--good) 40%, var(--line));
      }
      .tag-warn {
        color: var(--warn);
        border-color: color-mix(in srgb, var(--warn) 40%, var(--line));
      }
      .tag-bad {
        color: var(--bad);
        border-color: color-mix(in srgb, var(--bad) 40%, var(--line));
      }
      @media (max-width: 720px) {
        main {
          padding: var(--s-4);
        }
        .row {
          grid-template-columns: 1fr;
        }
      }
    </style>
  </head>
  <body>
    <main>
      <h1>Title</h1>
      <p class="muted">One-line context.</p>
      <!-- content -->
    </main>
    <script>
      // interactivity here, plain JS only
    </script>
  </body>
</html>
```

This scaffold is the minimum. Add only what the artifact needs.

## File naming and location

- Slug-case: `<topic>-<kind>-<YYYY-MM-DD>.html`. Examples: `auth-options-comparison-2026-05-13.html`, `incident-2026-05-12-postmortem.html`.
- Default location: `/tmp/` on macOS/Linux, or a `tmp/` folder in the current repo if the artifact is repo-related and the repo has a `tmp/` convention.
- Always print the absolute path to the user after writing.

## Export button pattern

For any artifact with editable state (drag-drop boards, toggleable flags, form-like UIs), include an Export button that serialises current state to a textarea the user can copy:

```html
<button id="exportBtn">Export</button>
<dialog id="exportDialog">
  <h3>Copy this back to chat</h3>
  <textarea id="exportOut" rows="12" cols="60" readonly></textarea>
  <button id="exportClose">Close</button>
</dialog>
<script>
  exportBtn.onclick = () => {
    exportOut.value = serializeState();
    exportDialog.showModal();
    exportOut.select();
  };
  exportClose.onclick = () => exportDialog.close();
  function serializeState() {
    /* return JSON or markdown */
  }
</script>
```

This is the human-in-the-loop hinge: the artifact does the manipulation, the user pipes the result back as text.

## What to avoid

- Inline `style="…"` attributes everywhere — keep styles in the single `<style>` block, use classes.
- `<br>` for spacing — use margin.
- Pixel-perfect fixed widths — use grid with `minmax()`.
- jQuery — modern DOM APIs are enough.
- Animations that play forever — they distract; let them play once or on hover.
- Color-only signalling — pair color tags with text or icons for accessibility.
