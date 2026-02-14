---
name: 'step-01b-continue'
description: 'Handle workflow continuation from a previous session'

outputFile: '{output_folder}/scoping-report-{project_name}.md'
step02: './step-02-triage.md'
step03: './step-03-functional-scoping.md'
step04: './step-04-architecture-estimation.md'
step05: './step-05-synthesis.md'
step06: './step-06-completion.md'
---

# Step 1b: Continue Workflow

## STEP GOAL:

To resume the feature scoping workflow from where it was left off in a previous session.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Step-Specific Rules:

- 🎯 Focus ONLY on detecting progress and routing to the correct step
- 🚫 FORBIDDEN to redo completed work
- 💬 Brief status update, then route immediately

## EXECUTION PROTOCOLS:

- 🎯 Read output file frontmatter to determine progress
- 💬 Report status to user before routing
- 📖 Do NOT update stepsCompleted — this step is a router, not a producer
- 🚫 FORBIDDEN to load next step until progress is confirmed

## CONTEXT BOUNDARIES:

- User has run this workflow before
- Output file exists with `stepsCompleted` array
- Need to route to the correct next step
- Per-feature files may already exist in `features/` directory

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly.

### 1. Read Progress

Load `{outputFile}` and read the frontmatter:
- `stepsCompleted` array
- `lastStep`
- `status`
- `total_features_input`, `total_features_scoped`, `total_features_killed`

### 2. Welcome Back

"**Welcome back!** Let me check where we left off...

**Progress:**
- Steps completed: [list from stepsCompleted]
- Features input: [count]
- Features scoped: [count]
- Last step: [lastStep]

Resuming from the next step."

### 3. Route to Next Step

Based on the last completed step, load the next step:

| Last Completed | Next Step | File |
|---|---|---|
| step-01-init | Triage | `{step02}` |
| step-02-triage | Functional Scoping | `{step03}` |
| step-03-functional-scoping | Architecture + Estimation | `{step04}` |
| step-04-architecture-estimation | Synthesis | `{step05}` |
| step-05-synthesis | Completion | `{step06}` |

Load, read entire file, then execute the appropriate next step.

### 4. Handle Edge Cases

- **If stepsCompleted is empty:** Route back to step-02 (triage) — init was completed but nothing else
- **If step-04 was partially completed:** Check `features/` directory for existing per-feature files. Report which features are done and which remain. The step-04 loop should pick up where it left off.
- **If all steps completed:** "This scoping report is already complete. To start a new one, rename or move the existing report."

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Progress correctly detected from output file
- User informed of current status
- Routed to correct next step
- No completed work redone

### ❌ SYSTEM FAILURE:

- Re-running completed steps
- Not reading the output file frontmatter
- Routing to the wrong step
- Not detecting partially completed step-04 loop

**Master Rule:** Detect, report, route. Don't redo work.
