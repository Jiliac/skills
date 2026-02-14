---
name: 'step-01-init'
description: 'Initialize the feature scoping workflow, gather inputs, and create the scoping report'

nextStepFile: './step-02-triage.md'
continueFile: './step-01b-continue.md'
outputFile: '{output_folder}/scoping-report-{project_name}.md'
templateFile: '../templates/scoping-report-template.md'
featuresDir: '{output_folder}/features'
---

# Step 1: Initialization

## STEP GOAL:

To initialize the feature scoping workflow, check for existing sessions, gather the feature list and any available context (architecture docs, codebase), and create the scoping report document.

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
- ✅ You bring systematic analysis and estimation expertise, user brings codebase knowledge and consulting judgment
- ✅ Together we produce defensible, architecture-grounded estimates

### Step-Specific Rules:

- 🎯 Focus ONLY on initialization and input gathering
- 🚫 FORBIDDEN to start triaging or analyzing features in this step
- 💬 Be direct — ask for what you need, don't over-explain the workflow
- 🚪 Create the report document and features directory before proceeding

## EXECUTION PROTOCOLS:

- 🎯 Check for continuation FIRST before anything else
- 💾 Create output file from template when inputs are gathered
- 📖 Update frontmatter stepsCompleted when complete
- 🚫 This is the init step — sets up everything that follows

## CONTEXT BOUNDARIES:

- This is the first step — no prior context in the workflow
- User may provide: feature list, architecture docs, codebase path, client constraints
- Only a feature list is required — everything else is optional
- Don't judge or analyze the feature list yet — that's triage (step 02)

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Check for Existing Session

Look for an existing file at `{outputFile}`.

- **If found** and it has a non-empty `stepsCompleted` array → load and execute `{continueFile}`
- **If not found** or `stepsCompleted` is empty → continue to step 2 below

### 2. Welcome and Gather Feature List

"**Let's scope some features.**

I need a few things from you:

**Required:**
- Your feature list — paste it, link a file, or describe them

**Optional (provide whatever you have):**
- Architecture docs or codebase path
- Client constraints (budget, timeline, team size)
- Any existing specs or notes

What are we working with?"

Wait for user input. Collect:
- The feature list (however it arrives — Notion export, bullet points, screenshot description, file path)
- Any optional context provided

### 3. Parse and Confirm Feature List

Extract individual features from whatever format the user provides. Present them back:

"**I see [N] features:**

| # | Feature | Source Notes |
|---|---------|-------------|
| 1 | [name] | [any context from the list] |
| 2 | [name] | ... |
| ... | ... | ... |

Did I capture them all correctly? Any to add or rename?"

Wait for confirmation. Adjust as needed.

### 4. Note Available Context

Summarize what context is available:

"**Context available:**
- Architecture docs: [yes — path / no]
- Codebase access: [yes — path / no]
- Client constraints: [summary / none provided]
- Other: [anything else]

This affects how deep the architecture delta analysis can go. [If no docs/codebase: We'll work with what we have — estimates will be higher confidence where we have context, lower where we don't.]"

### 5. Create Report and Features Directory

Create the scoping report from `{templateFile}` at `{outputFile}`:
- Fill in frontmatter: `date`, `user_name`, `project_name`, `total_features_input`
- Replace `{{project_name}}`, `{{date}}`, `{{user_name}}` in the template

Create the `{featuresDir}` directory for per-feature files.

### 6. Proceed to Triage

"**Setup complete.** Report created. Moving to triage — we'll walk through each feature and decide what to scope, kill, or split."

**Proceeding to triage...**

#### Menu Handling Logic:

- After setup complete and report created, update `stepsCompleted` in `{outputFile}` frontmatter to include `'step-01-init'` and set `lastStep: 'step-01-init'`, then immediately load, read entire file, then execute `{nextStepFile}`

#### EXECUTION RULES:

- This is an auto-proceed step with no user choices at the end
- Proceed directly to triage after initialization

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Continuation detection performed
- Feature list gathered and confirmed with user
- Available context noted
- Scoping report created from template at correct location
- Features directory created
- Ready to proceed to triage

### ❌ SYSTEM FAILURE:

- Starting to analyze or triage features in this step
- Not checking for continuation first
- Not confirming the feature list with the user
- Creating output files in wrong location
- Proceeding without a feature list

**Master Rule:** Initialize and gather inputs. Don't analyze yet. That's triage.
