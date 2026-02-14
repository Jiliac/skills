---
name: 'step-05-synthesis'
description: 'Compile synthesis from all per-feature files into the main report'

nextStepFile: './step-06-completion.md'
outputFile: '{output_folder}/scoping-report-{project_name}.md'
featuresDir: '{output_folder}/features'
---

# Step 5: Synthesis

## STEP GOAL:

To read all per-feature files and compile a synthesis section — summary table, sequencing recommendation, trade-off analysis, and open questions — into the main report.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a technical estimator and consulting advisor
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring synthesis and strategic recommendation expertise, user brings client relationship context and business priorities

### Step-Specific Rules:

- 🎯 Compile from existing data — do NOT re-analyze or re-estimate features
- 🚫 FORBIDDEN to change estimates or debug risk at this stage
- 💬 Present synthesis for user review — they may adjust priorities or recommendations
- 📖 Read ALL per-feature files from {featuresDir} before compiling

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append synthesis sections to {outputFile} under `## Estimation Summary` and `## Recommendations`
- 📖 Update frontmatter `stepsCompleted` and `lastStep` when complete

## CONTEXT BOUNDARIES:

- All per-feature files in {featuresDir} contain confirmed architecture deltas and estimates
- Main report has triage summary and FR sections from earlier steps
- This step COMPILES — it doesn't create new analysis
- Output must be readable by non-technical product owners for decision-making
- Debug risk is NOT included in the synthesis output — it's already baked into the estimate ranges

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load All Feature Data

Read every file in `{featuresDir}`. Extract from each:
- Feature name
- Estimate: optimistic / expected / pessimistic
- Dependencies
- Debug risk (internal reference only — not for output)

Read `{outputFile}` for the triage summary and feature context.

### 2. Build Summary Table

Compile the estimation summary table:

"**Estimation Summary**

| # | Feature | Expected (days) | Range | Confidence | Dependencies |
|---|---------|-----------------|-------|------------|-------------|
| 1 | [name] | [N] | [opt]-[pess] | [High/Medium/Low] | [list] |
| ... | ... | ... | ... | ... | ... |

**Totals:**
- Expected: [N] days
- Range: [opt total]-[pess total] days"

Confidence is derived from range width: tight range = High, moderate = Medium, wide = Low. Do NOT label it as "debug risk."

### 3. Sequencing Recommendation

Based on dependencies and priorities, recommend a build order:

"**Recommended Sequence:**

1. **[feature]** — [reason: no dependencies / enables others / highest value]
2. **[feature]** — [reason]
3. ...

**Rationale:** [Brief explanation of sequencing logic — dependency chains, risk reduction, value delivery]"

### 4. Trade-Off Analysis

Provide options for tighter timelines:

"**If timeline is tight:**
- **Cut [feature]** — saves [N] days, impact: [what you lose]
- **Reduce scope of [feature]** — drop [specific FRs], saves [N] days
- **Defer [feature]** to phase 2 — [reason it can wait]

**If budget allows more:**
- **Add [killed feature back]** — [N] additional days, value: [what you gain]"

### 5. Open Questions

List unresolved items for the client:

"**Open Questions:**
- [Question about a feature's scope or priority]
- [External dependency that needs confirmation]
- [Assumption that should be validated with stakeholders]"

### 6. Present Synthesis for Review

Present the complete synthesis to the user:

"**Synthesis complete.** Please review the summary table, sequencing, and trade-offs above. Anything to adjust before we finalize?"

Wait for user review and adjustments.

### 7. Present MENU OPTIONS

Display: "**Synthesis Complete - Select:** [C] Continue to Completion"

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

#### Menu Handling Logic:

- IF C: Append synthesis sections to {outputFile} under `## Estimation Summary` and `## Recommendations`, update frontmatter `stepsCompleted` to include `'step-05-synthesis'`, set `lastStep: 'step-05-synthesis'`, update `total_estimate_days_expected` with the expected total, then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then [Redisplay Menu Options](#7-present-menu-options)

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- All per-feature files read and compiled
- Summary table includes every scoped feature
- Totals calculated correctly
- Sequencing recommendation with clear rationale
- Trade-off options provided (cut/reduce/defer)
- Open questions listed
- Debug risk NOT surfaced in output (baked into ranges)
- Output readable by non-technical stakeholders

### ❌ SYSTEM FAILURE:

- Missing features from the summary table
- Re-analyzing or changing estimates at this stage
- Exposing debug risk labels in client-facing output
- Not providing sequencing or trade-off recommendations
- Producing output only a developer could understand

**Master Rule:** Compile, synthesize, recommend. Don't re-analyze. Make it client-ready.
