---
name: 'step-04-architecture-estimation'
description: 'Analyze architecture delta and produce estimates for each feature individually'

nextStepFile: './step-05-synthesis.md'
outputFile: '{output_folder}/scoping-report-{project_name}.md'
featuresDir: '{output_folder}/features'
featureTemplate: '../templates/feature-delta-template.md'
estimationModel: '../data/estimation-model.md'
advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'
partyModeWorkflow: '{project-root}/_bmad/core/workflows/party-mode/workflow.md'
---

# Step 4: Architecture Delta & Estimation

## STEP GOAL:

To analyze the architecture delta and produce risk-adjusted estimates for each feature, creating individual per-feature files with structured analysis.

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
- ✅ You bring architecture analysis and estimation framework expertise, user brings codebase knowledge and implementation experience
- ✅ Together we produce defensible, architecture-grounded estimates

### Step-Specific Rules:

- 🎯 Follow the per-feature analysis framework EXACTLY — architecture delta first, then sub-task decomposition, then estimate
- 🚫 FORBIDDEN to estimate without analyzing the architecture delta first — the delta IS the reasoning
- 💬 For each feature: propose the analysis, user validates and adjusts from experience
- 📖 Load {estimationModel} and {featureTemplate} before starting the loop
- 🔄 Process ALL features without pausing between them — maintain momentum

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Create one file per feature in {featuresDir} using {featureTemplate}
- 📖 Update frontmatter `stepsCompleted` and `lastStep` when ALL features are done
- 📖 Update `total_features_scoped` and `total_estimate_days_expected` in {outputFile} frontmatter

## CONTEXT BOUNDARIES:

- FRs from step-03 define WHAT each feature does
- Architecture docs and/or codebase may be available for delta analysis
- If no architecture docs: work from what the user can describe about the codebase
- The estimation model defines the cost structure — fixed spec cost + debug risk padding
- Debug risk is INTERNAL — it inflates the estimate range but is not surfaced to client
- Per-feature files go in {featuresDir}, one per feature

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Framework and Context

Read `{estimationModel}` for the cost model. Read `{featureTemplate}` for the per-feature output structure. Read `{outputFile}` to get the feature list and FRs from previous steps.

"**Architecture delta and estimation.** We'll go through each feature one by one:

1. **Architecture delta** — what exists, what extends, what's new, what's unknown
2. **Sub-task decomposition** — at 0.5-day granularity
3. **Estimate** — optimistic / expected / pessimistic with debug risk baked in

I'll analyze each feature and propose the breakdown. You validate and adjust from your knowledge of the codebase.

[N] features to process. Let's go."

### 2. Per-Feature Loop

For EACH scoped feature, perform this analysis:

#### a) Architecture Delta

Analyze against the existing codebase/architecture docs:

- **What Exists:** Services, endpoints, UI components, DB tables that already handle part of this
- **What Needs Extending:** Existing code that needs modification. Note complexity: trivial / moderate / significant
- **What's New:** Entirely new modules, services, patterns. Flag architectural novelty
- **Unknowns:** External APIs to evaluate, libraries to research, design decisions needing prototyping

If architecture docs are available, reference specific files, services, or patterns. If not, work from the user's description and note where assumptions are made.

#### b) Sub-Task Decomposition

Break the feature into sub-tasks at 0.5-day granularity:

| # | Sub-Task | Days | Notes |
|---|----------|------|-------|
| 1 | [task] | [0.5-N] | [context] |

Include spec writing time (~0.25 days per story/sub-task).

#### c) Debug Risk Assessment

Based on the architecture delta, assess debug risk using `{estimationModel}`:

- **Low:** Well-understood patterns, existing similar code, no external deps → +0-25% padding
- **Medium:** New patterns in known framework, moderate complexity → +25-75% padding
- **High:** Architectural novelty, external APIs, unclear requirements, tech debt → +75-200% padding

State the risk level and the specific triggers that drive it.

#### d) Estimate

Apply the estimation model:

| Scenario | Days | Rationale |
|----------|------|-----------|
| Optimistic | [N] | Clean execution, no debug |
| Expected | [N] | Risk-adjusted (debug risk baked in) |
| Pessimistic | [N] | Unknowns materialize |

#### e) Present and Confirm

Present the complete analysis for this feature. Wait for user to review and adjust. Common adjustments:
- "That existing service is more complex than you think" → increase estimate
- "We already have a pattern for this" → decrease estimate
- "This unknown is actually well-documented" → lower debug risk

#### f) Write Per-Feature File

After user confirms, create `{featuresDir}/feature-{name}.md` from {featureTemplate} with the confirmed analysis. Update the feature file frontmatter with estimate values and debug risk.

**Then immediately move to the next feature.** Do NOT pause or present a menu between features.

### 3. Loop Summary

After ALL features are processed:

"**Architecture delta and estimation complete.**

| # | Feature | Expected (days) | Range | Debug Risk |
|---|---------|-----------------|-------|------------|
| 1 | [name] | [N] | [opt]-[pess] | [Low/Med/High] |
| ... | ... | ... | ... | ... |

**Total expected:** [N] days
**Total range:** [opt]-[pess] days
**Files created:** [N] per-feature files in features/

Ready for synthesis."

### 4. Present MENU OPTIONS

Display: "**Architecture & Estimation Complete - Select an Option:** [A] Advanced Elicitation [P] Party Mode [C] Continue to Synthesis"

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution, return to this menu

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask}, and when finished redisplay the menu
- IF P: Execute {partyModeWorkflow}, and when finished redisplay the menu
- IF C: Update {outputFile} frontmatter: add `'step-04-architecture-estimation'` to `stepsCompleted`, set `lastStep: 'step-04-architecture-estimation'`, update `total_features_scoped` and `total_estimate_days_expected`, then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then [Redisplay Menu Options](#4-present-menu-options)

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Estimation model loaded and applied consistently
- Every scoped feature has a per-feature file in {featuresDir}
- Architecture delta analyzed before estimating (delta IS the reasoning)
- Sub-tasks at 0.5-day granularity
- Debug risk assessed with specific triggers
- Estimate range provided (optimistic/expected/pessimistic)
- User validated each feature's analysis
- No pausing between features — maintained momentum

### ❌ SYSTEM FAILURE:

- Estimating without analyzing architecture delta first
- Skipping features
- Not creating per-feature files
- Surfacing debug risk as client-facing information (it's internal padding)
- Pausing or presenting menus between individual features
- Using vague sub-tasks ("implement feature" is not a sub-task)

**Master Rule:** The architecture delta justifies the estimate. No delta analysis = no estimate. Process all features, then present the menu.
