---
stepsCompleted:
  [
    "step-01-discovery",
    "step-02-classification",
    "step-03-requirements",
    "step-04-tools",
    "step-05-plan-review",
    "step-06-design",
    "step-07-foundation",
    "step-08-build-step-01",
    "step-09-build-all-steps",
  ]
created: 2026-02-13
status: BUILD_COMPLETE
approvedDate: 2026-02-13
---

# Workflow Creation Plan

## Discovery Notes

**User's Vision:**
A structured workflow for the consulting scoping phase — the gap between "client presents a list of features" and "we start writing PRDs and stories." It handles a batch of features (10-25) against an existing codebase, producing architecture-grounded estimates with an LLM-aware cost model. Designed for a boutique AI/LLM consulting practice (Jiliac Labs) where engagements involve multiple features at varying levels of clarity, existing codebases (often 30k+ lines), and clients who need defensible timelines.

**Who It's For:**
Senior AI/LLM developers operating as consultants. The workflow runner is both the architect and estimator — they bring codebase expertise and make the architecture decisions embedded in the estimates.

**What It Produces:**

- Triaged feature list (scope / clarify / kill / split)
- Functional requirements per feature (3-8 FRs each, with boundaries)
- Architecture delta analysis per feature (what exists, what extends, what's new, what's unknown)
- LLM-aware estimates per feature with the cost model:
  - Fixed spec cost (~2hrs/story)
  - Near-zero code generation time
  - Debug risk rating (Low/Medium/High) with reasons
  - Range: optimistic → expected → pessimistic
- Synthesis: priority recommendations, sequencing, trade-offs, open questions
- Client-ready output for decision-making meetings

**Key Insights:**

- Phase 0 (codebase orientation) is a precondition, not a workflow step. Assumes architecture docs and codebase map already exist (separate skill).
- LLM-era estimation model: code generation is fast, spec writing is fixed cost (~25% dev day), debugging is the unpredictable variable. Karpathy guidelines define spec quality that determines debug risk.
- Triage must be informed by architecture docs (not blind) — you can't kill or split features without knowing what the codebase already supports.
- Multi-feature-by-default is a core design principle. Existing frameworks force single-feature tunnels.
- Output must be client-facing — ready for a meeting with the product owner/CTO.
- Compatible with BMAD pipeline: approved features flow into /create-prd or /quick-spec.
- Senior Architect skill (alirezarezvani/claude-skills) is a useful reference for architecture assessment patterns but not directly included — different problem (designing architecture vs measuring delta).
- Karpathy guidelines inform spec quality standards that determine debug risk in estimation.
- Tri-modal (edit/validate) deliberately excluded — too heavy, LLM handles review/edit naturally.

## Classification Decisions

**Workflow Name:** feature-scoping
**Target Path:** bmad/bmb-creations/workflows/feature-scoping/

**4 Key Decisions:**

1. **Document Output:** true — produces a persistent scoping report with FRs, architecture deltas, estimates, and synthesis
2. **Module Affiliation:** standalone — sits upstream of BMM, uses only core features (Advanced Elicitation, Party Mode)
3. **Session Type:** continuable — 10-25 features against large codebases, massive token consumption, multi-session expected
4. **Lifecycle Support:** create-only — v1 focus on creation; edit/validate handled naturally by LLM in separate passes

**Structure Implications:**

- Needs `steps-c/` only (no steps-e/ or steps-v/)
- Needs `step-01-init.md` with continuation detection and `step-01b-continue.md` for resuming
- Needs `stepsCompleted` tracking in output frontmatter
- Needs output template for the scoping report
- Core variables only: `user_name`, `communication_language`, `document_output_language`, `output_folder`
- Portable: self-contained folder, installable via copy + manifest CSV line (see INSTALL.md)

## Requirements

**Flow Structure:**

- Pattern: mixed — batch phases + per-feature loop
- Flow: Triage (all) → Functional Scoping (all) → [Architecture Delta → Estimation] per feature → Synthesis (all)
- No blocking states: "Clarify" features get explicit assumptions and continue, never block
- No pausing between features in the per-feature loop — maintain momentum
- Estimated steps: ~7 (init, continue, triage, functional-scoping, architecture-delta, estimation, synthesis)

**User Interaction:**

- Style: mixed
  - Triage: highly collaborative (discussing kill/scope/split decisions)
  - Functional Scoping: collaborative (refining FRs together)
  - Architecture Delta: mostly autonomous (AI reads codebase/docs, surfaces findings, user validates)
  - Estimation: collaborative (AI proposes breakdown, user adjusts from experience)
  - Synthesis: mostly autonomous (AI compiles, user reviews)
- Decision points: triage dispositions, FR boundaries, estimate adjustments
- Checkpoint frequency: at phase transitions (BMAD standard menu)

**Inputs Required:**

- Required: feature list (however rough — Notion export, spreadsheet, bullet points)
- Optional (provide whatever exists):
  - Architecture documentation
  - Codebase access
  - Client constraints (budget, timeline, team size, priorities)
  - Existing specs or PRDs
  - Previous scoping reports
- No precondition validation — workflow adapts to available input

**Output Specifications:**

- Type: document (structured scoping report)
- Format: structured — consistent sections per feature, repeating format
- Key sections per feature: purpose, FRs with boundaries, architecture delta, estimate with range
- Summary table: all features with estimates, confidence, priority recommendation
- Frequency: single report per engagement/scoping session

**Success Criteria:**

- Every input feature has a disposition — nothing falls through the cracks
- Architecture delta justifies the estimate naturally (the delta IS the reasoning)
- Debug risk is baked into estimates (internal input, not client-facing) — inflates padding appropriately
- Assumptions are documented explicitly for unclear features
- Dependencies between features are surfaced
- Synthesis gives clear sequencing and priority recommendation
- Non-technical product owner can read the summary and make decisions

**Instruction Style:**

- Overall: mixed
- Collaborative phases (triage, scoping): intent-based — goals and principles, AI adapts
- Analytical phases (architecture delta, estimation, synthesis): prescriptive — specific instructions, read these docs, produce this format

## Tools Configuration

**Core BMAD Tools:**

- **Party Mode:** included — available at checkpoints for multi-perspective analysis on contentious decisions
- **Advanced Elicitation:** included — available at checkpoints for deep-dives
- **Brainstorming:** excluded — done separately as preparatory step, not part of this workflow

**LLM Features:**

- All implicit — this is a Claude Code workflow. File I/O, sub-agents, web browsing, sub-processes are naturally available and used as needed. No explicit configuration required.

**Memory:**

- Type: continuable
- Tracking: `stepsCompleted` array + `lastStep` in output frontmatter
- Resume via `step-01b-continue.md`

**External Integrations:** none

**Workflow Structure Preview:**

```
Phase 1: Initialization
  - Load config, detect continuation
  - Gather inputs: feature list, link architecture docs/codebase if available
  - Set up the scoping report document

Phase 2: Triage (batch - all features)
  - Classify: scope / scope-with-assumptions / kill / split
  - Surface dependencies between features

Phase 3: Functional Scoping (batch - all features)
  - Per feature: purpose statement, 3-8 FRs, explicit boundaries

Phase 4: Architecture Delta + Estimation (per-feature loop)
  - Per feature: what exists / extends / new / unknowns
  - Decompose into sub-tasks, apply estimation model
  - No pausing between features

Phase 5: Synthesis (batch - all features)
  - Summary table, sequencing, priority, trade-offs, open questions
```

## Workflow Design

### File Structure

```
feature-scoping/
├── workflow.md                          # Entry point, config loading, mode selection
├── INSTALL.md                           # Portability instructions
├── templates/
│   ├── scoping-report-template.md       # Main report template (triage + FRs + synthesis)
│   └── feature-delta-template.md        # Per-feature architecture delta + estimate template
├── data/
│   ├── estimation-model.md              # LLM-era cost model (spec cost, debug risk, padding rules)
│   └── triage-criteria.md               # Triage decision framework (scope/kill/split criteria)
└── steps-c/
    ├── step-01-init.md                  # Initialize, continuation detection, gather inputs
    ├── step-01b-continue.md             # Resume from previous session
    ├── step-02-triage.md                # Batch: classify all features
    ├── step-03-functional-scoping.md    # Batch: FRs + boundaries for all surviving features
    ├── step-04-architecture-estimation.md  # Per-feature loop: delta + estimate → individual files
    ├── step-05-synthesis.md             # Batch: compile summary from per-feature files
    └── step-06-completion.md            # Final review, polish, mark complete
```

### Output Structure

```
{output_folder}/
├── scoping-report-{project_name}.md     # Main report: triage + FRs + synthesis summary table
└── features/
    ├── feature-{name-a}.md              # Architecture delta + estimate for feature A
    ├── feature-{name-b}.md              # Architecture delta + estimate for feature B
    └── ...                              # One file per scoped feature
```

### Step Design Detail

#### step-01-init.md (Init, Continuable)

- **Type:** Init with continuation detection
- **Menu:** Auto-proceed
- **Goal:** Check for existing report (continuation), gather feature list + optional docs/codebase links, create report from template
- **Output:** Creates `scoping-report-{project_name}.md` from template, creates `features/` directory
- **Continuation:** If report exists with stepsCompleted → route to step-01b-continue.md

#### step-01b-continue.md (Continuation)

- **Type:** Continuation handler
- **Menu:** Auto-proceed
- **Goal:** Read stepsCompleted from existing report, welcome back, route to correct step
- **Output:** None (routing only)

#### step-02-triage.md (Middle, Standard)

- **Type:** Middle step, collaborative
- **Menu:** A/P/C
- **Goal:** Walk through all features collaboratively, classify each
- **Instruction style:** Intent-based — facilitate discussion, probe rationale
- **Classifications:** scope / scope-with-assumptions (document assumptions) / kill (document reason) / split (decompose, re-triage)
- **Loads:** `data/triage-criteria.md` for decision framework
- **Output:** Appends triaged feature table to main report
- **Data flow:** Produces the feature list that step-03 and step-04 consume

#### step-03-functional-scoping.md (Middle, Standard)

- **Type:** Middle step, collaborative
- **Menu:** A/P/C
- **Goal:** For each surviving feature: one-sentence purpose, 3-8 FRs, explicit boundaries (what's NOT included), dependencies
- **Instruction style:** Intent-based — collaborative refinement
- **Output:** Appends FR sections to main report (compact, per feature)
- **Data flow:** FRs inform architecture delta analysis in step-04

#### step-04-architecture-estimation.md (Middle, Standard — LOOP)

- **Type:** Middle step with per-feature loop
- **Menu:** A/P/C (at end of all features, not between)
- **Goal:** For each scoped feature: read relevant docs/code, analyze architecture delta, decompose sub-tasks, apply estimation model, produce estimate range
- **Instruction style:** Prescriptive — specific analysis framework, structured output format
- **Loads:** `data/estimation-model.md` for cost framework, `templates/feature-delta-template.md` for per-feature output
- **Output:** Creates one `features/feature-{name}.md` file per feature using template
- **Per-feature file contains:**
  - Architecture delta: what exists / what extends / what's new / unknowns
  - Sub-task decomposition at 0.5-day granularity
  - Debug risk assessment (internal — Low/Medium/High with reasons)
  - Estimate range: optimistic / expected / pessimistic (debug risk baked into padding)
  - Dependencies on other features
- **Loop behavior:** Process all features without pausing. Maintain momentum.

#### step-05-synthesis.md (Middle, Simple)

- **Type:** Middle step, mostly autonomous
- **Menu:** C only
- **Goal:** Read all per-feature files, compile summary table, produce sequencing recommendation, trade-off analysis, open questions
- **Instruction style:** Prescriptive — compile from existing data, structured format
- **Output:** Appends synthesis section to main report:
  - Summary table: feature name | estimate (days) | confidence | priority | dependencies
  - Sequencing recommendation (what to build first, why)
  - Trade-off analysis (what to cut for tighter timeline)
  - Open questions for client
  - Total estimate range

#### step-06-completion.md (Final)

- **Type:** Final step
- **Menu:** None
- **Goal:** Polish pass on main report, verify all features accounted for, update frontmatter to complete
- **Output:** Final report ready for client meeting

### Data Files

#### estimation-model.md

- Fixed spec cost: ~2hrs per story (~25% dev day)
- Code generation: near-zero (LLM writes it)
- Debug risk levels:
  - **Low:** Well-understood patterns, existing similar code, no external deps → minimal padding
  - **Medium:** New patterns within known framework, moderate complexity → +50% padding
  - **High:** Architectural novelty, external API integration, unclear requirements, tech debt interaction → +100-200% padding
- Estimate range formula: optimistic (no debug) / expected (risk-adjusted) / pessimistic (worst case)

#### triage-criteria.md

- **Scope:** Clearly needed, well-understood, feasible within constraints
- **Scope with assumptions:** Needed but unclear — state assumptions explicitly, continue
- **Kill:** Not needed for stated goal, or cost vastly exceeds value. Document reason.
- **Split:** Multiple features hiding under one label. Decompose, re-triage each.
- Questions to ask per feature: Is this one feature or several? Does the codebase already handle part of this? Is this v1 or v2?

### Role and Persona

- **Expertise:** Workflow architect + technical estimator + consulting advisor
- **Tone:** Direct, analytical, no fluff. Collaborative in triage/scoping, systematic in architecture/estimation.
- **Communication:** English (configurable). Speaks to both the developer running the workflow and produces output readable by non-technical stakeholders.

### Subprocess Optimization

- **Step 04 (architecture-estimation):** Could benefit from sub-agents for parallel feature analysis, but v1 keeps it sequential for simplicity. The per-feature file structure enables future parallelization.
- **Step 05 (synthesis):** Reads multiple files — natural fit for file I/O but no subprocess optimization needed for v1.

## Build Log

### Step 01 Build Complete

**Created:**

- steps-c/step-01-init.md
- steps-c/step-01b-continue.md

**Step Configuration:**

- Type: Init (Continuable) + Continuation handler
- Outputs to: Creates scoping report from template, creates features/ directory
- Next Step: step-02-triage.md

### Step 02 Build Complete

**Created:**

- steps-c/step-02-triage.md

**Step Configuration:**

- Type: Middle (Standard) — A/P/C menu
- Instruction style: Intent-based, collaborative
- Loads: data/triage-criteria.md
- Outputs to: Appends triage summary table to main report
- Next Step: step-03-functional-scoping.md

### Step 03 Build Complete

**Created:**

- steps-c/step-03-functional-scoping.md

**Step Configuration:**

- Type: Middle (Standard) — A/P/C menu
- Instruction style: Intent-based, collaborative
- Outputs to: Appends FR sections to main report
- Next Step: step-04-architecture-estimation.md

### Step 04 Build Complete

**Created:**

- steps-c/step-04-architecture-estimation.md

**Step Configuration:**

- Type: Middle (Standard) with per-feature LOOP — A/P/C menu at end only
- Instruction style: Prescriptive
- Loads: data/estimation-model.md, templates/feature-delta-template.md
- Outputs to: Creates per-feature files in features/ directory
- Next Step: step-05-synthesis.md

### Step 05 Build Complete

**Created:**

- steps-c/step-05-synthesis.md

**Step Configuration:**

- Type: Middle (Simple) — C only menu
- Instruction style: Prescriptive, compile from existing data
- Reads: All per-feature files from features/ directory
- Outputs to: Appends synthesis sections to main report
- Next Step: step-06-completion.md

### Step 06 Build Complete

**Created:**

- steps-c/step-06-completion.md

**Step Configuration:**

- Type: Final — no menu, no next step
- Outputs to: Updates main report frontmatter to COMPLETE
- Next Step: None (final step)
