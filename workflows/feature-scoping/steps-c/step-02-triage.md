---
name: "step-02-triage"
description: "Classify all features: scope, scope-with-assumptions, kill, or split"

nextStepFile: "./step-03-functional-scoping.md"
outputFile: "{output_folder}/scoping-report-{project_name}.md"
triageCriteria: "../data/triage-criteria.md"
advancedElicitationTask: "{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml"
partyModeWorkflow: "{project-root}/_bmad/core/workflows/party-mode/workflow.md"
---

# Step 2: Triage

## STEP GOAL:

To walk through every feature collaboratively and classify each as scope, scope-with-assumptions, kill, or split — producing a triaged feature table that determines what moves forward.

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
- ✅ You bring architecture awareness and systematic triage patterns, user brings domain knowledge and client context
- ✅ Together we decide what's worth scoping

### Step-Specific Rules:

- 🎯 Focus ONLY on classification — do NOT write FRs or estimate anything
- 🚫 FORBIDDEN to skip features — every single feature must get a classification
- 💬 Discuss each feature — ask triage questions, challenge assumptions, surface trade-offs
- 📖 Load {triageCriteria} before starting triage

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append triaged feature table to {outputFile} under `## Triage Summary`
- 📖 Update frontmatter `stepsCompleted` and `lastStep` when complete
- 📖 Update `total_features_killed` count in frontmatter

## CONTEXT BOUNDARIES:

- Feature list was gathered in step-01 and confirmed with user
- Architecture docs and/or codebase may be available (noted in step-01)
- Focus: classification only — not requirements, not estimates
- If architecture docs are available, reference them when discussing feasibility
- Dependencies between features should be surfaced but not deeply analyzed yet

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Triage Framework

Read `{triageCriteria}` to have the decision framework ready. Read `{outputFile}` to get the confirmed feature list from step-01.

### 2. Set Up Triage

"**Time to triage.** We'll go through each feature and decide: scope it, scope it with assumptions, kill it, or split it. I'll ask questions to surface issues — push back if you disagree.

**Classifications:**

- **Scope** — clear and ready to scope
- **Scope with assumptions** — unclear but we can proceed by stating assumptions
- **Kill** — not worth building, document why
- **Split** — multiple features hiding as one, decompose and re-triage

Let's go."

### 3. Walk Through Each Feature

For each feature, facilitate a collaborative triage discussion:

1. **State the feature** and any context from the original list
2. **Ask the triage questions** from {triageCriteria} that are relevant (not all 6 every time — use judgment):
   - Is this one feature or several?
   - Does the codebase already handle part of this?
   - Is this v1 or v2?
   - Who uses this?
   - What breaks without it?
   - Is this the right solution?
3. **If architecture docs are available**, reference relevant existing capabilities
4. **Propose a classification** with reasoning — but wait for user agreement
5. **If split:** list the sub-features and triage each immediately
6. **If scope-with-assumptions:** document each assumption explicitly ("Assuming X, not Y")
7. **If kill:** document the reason ("Killing because [reason]")

Do NOT rush through features. Each one deserves discussion. But don't over-analyze — that's what later steps are for.

### 4. Build Triage Summary Table

After all features are classified, present the complete triage table:

"**Triage complete.** Here's the summary:

| #   | Feature | Classification   | Assumptions | Dependencies | Notes    |
| --- | ------- | ---------------- | ----------- | ------------ | -------- |
| 1   | [name]  | [classification] | [if any]    | [if any]     | [if any] |
| ... | ...     | ...              | ...         | ...          | ...      |

**Counts:**

- Scoped: [N]
- Scoped with assumptions: [N]
- Killed: [N]
- Split into: [N] new features

[N] features moving forward to functional scoping."

Wait for user to review and confirm.

### 5. Present MENU OPTIONS

Display: "**Triage Complete - Select an Option:** [A] Advanced Elicitation [P] Party Mode [C] Continue to Functional Scoping"

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution, return to this menu

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask}, and when finished redisplay the menu
- IF P: Execute {partyModeWorkflow}, and when finished redisplay the menu
- IF C: Append triage summary table to {outputFile} under `## Triage Summary`, update frontmatter `stepsCompleted` to include `'step-02-triage'`, set `lastStep: 'step-02-triage'`, update `total_features_killed`, then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then [Redisplay Menu Options](#5-present-menu-options)

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Triage criteria loaded and applied
- Every feature classified — nothing skipped
- Each classification has reasoning
- Assumptions documented for "scope-with-assumptions" features
- Kill reasons documented
- Split features decomposed and re-triaged
- Dependencies between features surfaced
- Triage table appended to main report

### ❌ SYSTEM FAILURE:

- Skipping features during triage
- Classifying without discussion or reasoning
- Starting to write FRs or estimate in this step
- Not loading triage criteria
- Not documenting assumptions or kill reasons

**Master Rule:** Every feature gets a classification with reasoning. No skipping, no silent decisions.
