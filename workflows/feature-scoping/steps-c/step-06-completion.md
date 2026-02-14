---
name: 'step-06-completion'
description: 'Final review, polish, and mark the scoping report as complete'

outputFile: '{output_folder}/scoping-report-{project_name}.md'
featuresDir: '{output_folder}/features'
---

# Step 6: Completion

## STEP GOAL:

To perform a final polish pass on the main report, verify all features are accounted for, and mark the scoping report as complete.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a technical estimator and consulting advisor
- ✅ Final quality check before client delivery

### Step-Specific Rules:

- 🎯 Polish and verify — do NOT add new analysis or change estimates
- 🚫 FORBIDDEN to modify estimates, FRs, or classifications at this stage
- 💬 Present final report summary to user for sign-off

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Update {outputFile} frontmatter: set `status: "COMPLETE"`, ensure all counts are accurate
- 📖 This is the FINAL step — no next step file

## CONTEXT BOUNDARIES:

- Main report has all sections filled from steps 02-05
- Per-feature files exist in {featuresDir}
- This is a quality check, not a content creation step
- Output should be ready for a client meeting after this step

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load and Verify

Read `{outputFile}` completely. Read all files in `{featuresDir}`.

Verify:
- Every feature from the triage has a disposition (scope/kill/split)
- Every scoped feature has FRs in the report
- Every scoped feature has a per-feature file in {featuresDir}
- Summary table in synthesis matches per-feature files
- Totals are consistent (feature counts, estimate totals)

If any discrepancies found, report them to the user.

### 2. Polish Pass

Review the main report for:
- Consistent formatting across sections
- No orphaned references to killed or split features
- Triage, FR, and synthesis sections flow logically
- Summary table is complete and accurate
- Report reads well for a non-technical audience

Make minor formatting fixes. Do NOT change substance.

### 3. Final Summary

Present to the user:

"**Scoping report complete.**

**Report:** `{outputFile}`
**Per-feature files:** `{featuresDir}/` ([N] files)

**Summary:**
- Features input: [N]
- Features scoped: [N]
- Features killed: [N]
- Total expected: [N] days
- Total range: [opt]-[pess] days

The report is ready for your client meeting. Per-feature architecture deltas and detailed estimates are in the features directory for reference.

**Next steps in BMAD pipeline:** Approved features can go to `/create-prd` or `/quick-spec`."

### 4. Mark Complete

Update `{outputFile}` frontmatter:
- Set `status: "COMPLETE"`
- Ensure `stepsCompleted` includes `'step-06-completion'`
- Set `lastStep: 'step-06-completion'`
- Verify all counts: `total_features_input`, `total_features_scoped`, `total_features_killed`, `total_estimate_days_expected`

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- All features accounted for (none missing)
- Counts and totals are consistent
- Report is polished and client-ready
- Frontmatter marked as COMPLETE
- User informed of output file locations
- BMAD pipeline next steps mentioned

### ❌ SYSTEM FAILURE:

- Missing features in the final report
- Inconsistent totals or counts
- Modifying estimates or analysis at this stage
- Not marking the report as complete
- Leaving formatting issues in the report

**Master Rule:** Verify, polish, complete. Don't change substance — just make sure everything is there and clean.
