# Pattern Recipes

Each pattern: when to use, minimal recipe, pitfalls. Drop into the scaffold from `architecture.md`.

**Contents**

1. Side-by-side option comparison
2. Annotated diff
3. Module / architecture map
4. Design-token swatches & component contact sheet
5. Animation / easing sandbox
6. Clickable multi-screen flow
7. Long-form doc with progressive disclosure
8. Post-mortem timeline
9. Plan / proposal timeline
10. Drag-and-drop board with Export

## 1. Side-by-side option comparison

**When:** presenting 2–4 approaches the user must choose between.

**Recipe:** a `.row` grid of `.panel` cards, each with a title, one-line summary, pros/cons list, and a "pick this if" tag.

```html
<section class="row">
  <article class="panel">
    <h3>Option A — Session cookies</h3>
    <p>Server-issued, HttpOnly, SameSite=Lax.</p>
    <ul>
      <li class="tag tag-good">Simple</li>
      <li class="tag tag-warn">Stateful server</li>
    </ul>
    <p class="muted">Pick this if you control both client and server.</p>
  </article>
  <article class="panel">…</article>
</section>
```

**Pitfalls:** equal-length pro/con lists feel padded; let one side be shorter when honest. Don't bury the recommendation — mark one card as `class="panel recommended"` with a thicker accent border.

## 2. Annotated diff

**When:** explaining a code change, code review, or before/after.

**Recipe:** two columns of `<pre>` with line numbers, plus a margin column with notes keyed to line numbers.

```html
<section class="diff">
  <pre class="diff-old"><code>line 1
- line 2
  line 3</code></pre>
  <pre class="diff-new"><code>line 1
+ refactored line 2
  line 3</code></pre>
  <aside class="diff-notes">
    <p data-line="2">
      <span class="tag tag-warn">Behavior</span> Now async; callers must await.
    </p>
  </aside>
</section>
```

CSS: `.diff { display: grid; grid-template-columns: 1fr 1fr 280px; }`, color `+` lines green and `-` lines red via line-level spans.

**Pitfalls:** copy-paste-killing line numbers — put them in a `::before` pseudo-element or a separate gutter column so users can copy raw code. Highlight only the changed lines, not entire blocks.

## 3. Module / architecture map

**When:** describing how components, services, or files relate.

**Recipe:** inline SVG with `<rect>` nodes and `<path>` edges. Author by hand for small graphs (<15 nodes); for larger, use D3 from a CDN.

```html
<svg viewBox="0 0 800 400" role="img" aria-label="Module map">
  <defs>
    <marker
      id="arrow"
      viewBox="0 0 10 10"
      refX="9"
      refY="5"
      markerWidth="6"
      markerHeight="6"
      orient="auto"
    >
      <path d="M0,0 L10,5 L0,10 z" fill="currentColor" />
    </marker>
  </defs>
  <g font-family="var(--font-sans)" font-size="13">
    <rect
      x="40"
      y="40"
      width="160"
      height="60"
      rx="10"
      fill="var(--panel)"
      stroke="var(--line)"
    />
    <text x="120" y="75" text-anchor="middle" fill="var(--ink)">api/auth</text>
    <path
      d="M200,70 L320,70"
      stroke="currentColor"
      fill="none"
      marker-end="url(#arrow)"
    />
  </g>
</svg>
```

**Pitfalls:** auto-routed edges that cross — accept a few overlaps rather than wiggle. Use color sparingly; reserve a single accent for "hot path."

## 4. Design-token swatches & component contact sheet

**When:** documenting a design system or proposing one.

**Recipe:** a grid of swatch tiles for color; a stacked list of type samples; a contact sheet of every variant of a component on one page.

```html
<section class="row">
  <div class="panel" style="background:#7c9cff">
    <code>--accent</code><br /><code>#7c9cff</code>
  </div>
  …
</section>
<section>
  <p style="font-size:48px">Aa — Display</p>
  <p style="font-size:28px">Aa — Heading</p>
  <p style="font-size:15px">Aa — Body</p>
</section>
```

**Pitfalls:** swatches without hex/token name are useless — always label both. For components, show every state (default/hover/active/disabled) and every size, in a single sweep.

## 5. Animation / easing sandbox

**When:** picking a transition, easing curve, or duration.

**Recipe:** one card with the animated element, controls for duration and easing, a "Play" button.

```html
<div class="sandbox">
  <div id="box" class="anim-target"></div>
  <label
    >Duration <input id="dur" type="range" min="100" max="2000" value="400"
  /></label>
  <label
    >Easing
    <select id="ease">
      <option>ease</option>
      <option>ease-in-out</option>
      <option>cubic-bezier(0.2, 0.8, 0.2, 1)</option>
    </select>
  </label>
  <button id="play">Play</button>
</div>
<script>
  play.onclick = () => {
    box.style.transition = `transform ${dur.value}ms ${ease.value}`;
    box.style.transform =
      box.style.transform === "translateX(300px)"
        ? "translateX(0)"
        : "translateX(300px)";
  };
</script>
```

**Pitfalls:** auto-playing animations are exhausting — require an explicit Play click. Show the resulting CSS `transition` string in a `<code>` block so the user can copy it.

## 6. Clickable multi-screen flow

**When:** evaluating a UX flow with 3–8 screens.

**Recipe:** `<dialog>` or hidden `<section>` per screen; buttons inside each advance to the next; a progress dots row at the top.

**Pitfalls:** building real validation — don't. The flow only needs to demonstrate the path; inputs can accept anything. Add a "reset" button.

## 7. Long-form doc with progressive disclosure

**When:** a spec, RFC, or proposal that's >2 screens long.

**Recipe:** TL;DR `<aside>` at the top; section headings with `<details>` for deep dives; tabbed code samples via radio buttons; hover-linked glossary using `<abbr>` or `<dfn>` with a `title`.

```html
<aside class="panel" style="border-left: 3px solid var(--accent)">
  <strong>TL;DR.</strong> One-paragraph summary the user could quote.
</aside>

<details>
  <summary>Why this approach</summary>
  <p>…</p>
</details>

<dfn title="Token issued on login, sent with every request">JWT</dfn>
```

**Pitfalls:** putting the recommendation in the deepest `<details>` — surface it in the TL;DR. Tabs that hide critical info make the user click to discover; default-expand the most likely tab.

## 8. Post-mortem timeline

**When:** writing up an incident, regression, or outage.

**Recipe:** a vertical timeline (a flex column with timestamp gutters), log excerpts in `<pre>` blocks at the relevant timestamp, an action-items checklist at the bottom.

```html
<ol class="timeline">
  <li>
    <time>14:02</time>
    <div><strong>Alert fired.</strong> p99 latency > 2s.</div>
  </li>
  <li>
    <time>14:05</time>
    <div><pre>500 status from /api/checkout</pre></div>
  </li>
  <li>
    <time>14:18</time>
    <div>Rollback to v1.42 — mitigated.</div>
  </li>
</ol>
<h2>Action items</h2>
<ul>
  <li><input type="checkbox" /> Add staged-rollout for /api/checkout</li>
</ul>
```

**Pitfalls:** mixing speculation with facts — keep "what happened" and "why we think it happened" in visually distinct lanes (different background, or a left-side tag).

## 9. Plan / proposal timeline

**When:** proposing a multi-week or multi-phase plan.

**Recipe:** horizontal timeline with milestones, embedded mini-diagrams for data flow, risk callouts as red panels, owner avatars or initials at each milestone.

**Pitfalls:** vague milestone names ("Phase 2: improvements"). Name milestones by the artifact produced ("Phase 2: migration tool merged to main").

## 10. Drag-and-drop board with Export

**When:** triaging tickets, ordering features, sorting any list with a structure the user wants to manipulate.

**Recipe:** native HTML drag-and-drop API (`draggable="true"`, `dragstart`, `dragover`, `drop`). Columns are `<section>` elements; items are `<article>` elements. Export button serialises columns to a JSON or markdown list.

```html
<section class="column" data-col="now">
  <h3>Now</h3>
  <article draggable="true" data-id="t1">Triage auth bug</article>
</section>
<button id="export">Export</button>
<script>
  document.querySelectorAll('article[draggable]').forEach(el => {
    el.addEventListener('dragstart', e => e.dataTransfer.setData('text/plain', el.dataset.id));
  });
  document.querySelectorAll('.column').forEach(col => {
    col.addEventListener('dragover', e => e.preventDefault());
    col.addEventListener('drop', e => {
      const id = e.dataTransfer.getData('text/plain');
      col.appendChild(document.querySelector(`[data-id="${id}"]`));
    });
  });
  export.onclick = () => {
    const out = [...document.querySelectorAll('.column')].map(c =>
      `## ${c.querySelector('h3').textContent}\n` +
      [...c.querySelectorAll('article')].map(a => `- ${a.textContent.trim()}`).join('\n')
    ).join('\n\n');
    navigator.clipboard.writeText(out);
    alert('Copied to clipboard.');
  };
</script>
```

**Pitfalls:** native drag-and-drop is fine for prototypes but does not work on touch devices without polyfill. State this limitation in the artifact's TL;DR if relevant.
