# Installing the Feature Scoping Workflow

## Prerequisites

- A project with BMAD installed (core module minimum)
- The `_config/workflow-manifest.csv` file in the target project

## Installation Steps

### 1. Copy the workflow folder

Copy the entire `feature-scoping/` folder (excluding this INSTALL.md and the workflow-plan file) into your target project:

```bash
cp -r feature-scoping/ <target-project>/_bmad/custom/workflows/feature-scoping/
```

The folder structure to copy:

```
feature-scoping/
├── workflow.md
├── data/
├── templates/
└── steps-c/
    ├── step-01-triage.md
    ├── step-02-functional-scoping.md
    └── ...
```

### 2. Register in the workflow manifest

Add this line to `<target-project>/_bmad/_config/workflow-manifest.csv`:

```csv
"feature-scoping","Scope, estimate, and prioritize a batch of features against an existing codebase","custom","_bmad/custom/workflows/feature-scoping/workflow.md"
```

### 3. Register the Claude Code slash command

Create the file `<target-project>/.claude/commands/bmad/custom/workflows/feature-scoping.md` with:

```markdown
---
description: "Scope, estimate, and prioritize a batch of features against an existing codebase"
---

IT IS CRITICAL THAT YOU FOLLOW THIS COMMAND: LOAD the FULL @\_bmad/custom/workflows/feature-scoping/workflow.md, READ its entire contents and follow its directions exactly!
```

This is what makes `/feature-scoping` available as a slash command in Claude Code. Without it, the workflow is registered in BMAD but not exposed to the IDE.

### 4. Verify

Restart Claude Code. The workflow should now be available via `/feature-scoping`.

## Notes

- This workflow is standalone — it depends only on BMAD core (Advanced Elicitation, Party Mode).
- No BMM or other module variables are required.
- The workflow assumes codebase orientation is already done (architecture docs exist). If they don't, run `document-project` or equivalent first.
