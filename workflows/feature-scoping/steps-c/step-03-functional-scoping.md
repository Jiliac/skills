---
name: 'step-03-functional-scoping'
description: 'Define functional requirements and boundaries for all surviving features'

nextStepFile: './step-04-architecture-estimation.md'
outputFile: '{output_folder}/scoping-report-{project_name}.md'
advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'
partyModeWorkflow: '{project-root}/_bmad/core/workflows/party-mode/workflow.md'
---

# Step 3: Functional Scoping

## STEP GOAL:

To define functional requirements and explicit boundaries for every surviving feature — producing the FR sections that inform architecture delta analysis.

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
- ✅ You bring structured analysis and FR decomposition expertise, user brings domain knowledge and client expectations
- ✅ Together we define what each feature actually means

### Step-Specific Rules:

- 🎯 Focus ONLY on functional requirements and boundaries — do NOT analyze architecture or estimate
- 🚫 FORBIDDEN to skip features that were classified as "scope" or "scope-with-assumptions"
- 💬 Collaborative refinement — propose FRs, user validates and adjusts
- 📖 Reference triage assumptions for "scope-with-assumptions" features

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append FR sections to {outputFile} under `## Functional Requirements`
- 📖 Update frontmatter `stepsCompleted` and `lastStep` when complete

## CONTEXT BOUNDARIES:

- Triage table from step-02 tells us which features survived and with what assumptions
- Focus: what each feature DOES, not how it's built
- Boundaries are as important as requirements — state what's explicitly NOT included
- Dependencies noted in triage should inform FR definitions
- Keep FRs testable and specific — no vague "should be user-friendly" type requirements

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Context

Read `{outputFile}` to get the triage summary. Identify all features classified as "scope" or "scope-with-assumptions."

"**Moving to functional scoping.** We have [N] features to define. For each one, we'll nail down:
- **Purpose** — one sentence, what problem does it solve
- **FRs** — 3-8 functional requirements, specific and testable
- **Boundaries** — what's explicitly NOT included
- **Dependencies** — what this feature needs from others

Let's work through them."

### 2. Scope Each Feature

For each surviving feature, collaboratively define:

**a) Purpose Statement**
One sentence: what problem does this solve, for which user?

**b) Functional Requirements (3-8)**
- Each FR should be specific and testable
- Start with a verb: "Allow users to...", "Display...", "Validate...", "Send..."
- Avoid vague requirements — "easy to use" is not an FR
- For "scope-with-assumptions" features, explicitly tie FRs to the stated assumptions

**c) Boundaries (what's NOT included)**
- State what this feature explicitly does NOT do in v1
- This prevents scope creep during implementation
- Example: "Does NOT include bulk upload — single item only"

**d) Dependencies**
- Other features this one depends on
- External systems or APIs involved

Present each feature's scope to the user for confirmation before moving to the next.

### 3. Compile FR Summary

After all features are scoped, present a compact summary:

"**Functional scoping complete.**

| # | Feature | FRs | Boundaries | Dependencies |
|---|---------|-----|------------|-------------|
| 1 | [name] | [count] | [count] | [list] |
| ... | ... | ... | ... | ... |

Total: [N] features scoped with [total FRs] functional requirements.

These FRs will drive the architecture delta analysis next."

Wait for user to review.

### 4. Present MENU OPTIONS

Display: "**Functional Scoping Complete - Select an Option:** [A] Advanced Elicitation [P] Party Mode [C] Continue to Architecture & Estimation"

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution, return to this menu

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask}, and when finished redisplay the menu
- IF P: Execute {partyModeWorkflow}, and when finished redisplay the menu
- IF C: Append FR sections for all features to {outputFile} under `## Functional Requirements`, update frontmatter `stepsCompleted` to include `'step-03-functional-scoping'`, set `lastStep: 'step-03-functional-scoping'`, then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then [Redisplay Menu Options](#4-present-menu-options)

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Every surviving feature has a purpose statement
- Each feature has 3-8 specific, testable FRs
- Boundaries are explicitly stated for each feature
- Dependencies identified
- "Scope-with-assumptions" features have FRs tied to stated assumptions
- FR sections appended to main report

### ❌ SYSTEM FAILURE:

- Skipping features from the triage
- Writing vague, untestable FRs
- Not stating boundaries (what's NOT included)
- Starting architecture analysis or estimation in this step
- Not referencing triage assumptions for unclear features

**Master Rule:** Define what it does, what it doesn't, and what it depends on. Don't design the how — that's architecture.
