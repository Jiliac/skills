# Triage Decision Framework

## Classifications

### Scope

Feature is clearly needed, well-understood, and feasible within constraints. Proceed to functional scoping.

**Indicators:**

- Direct connection to stated project goals
- Requirements are clear enough to write FRs
- No major unknowns that would prevent estimation
- Reasonable complexity relative to timeline

### Scope with Assumptions

Feature is needed but unclear in some dimension. State assumptions explicitly and proceed.

**Indicators:**

- Valuable but requirements are vague or ambiguous
- Multiple interpretations possible
- Needs client conversation to finalize, but we can make reasonable assumptions
- Architecture impact is estimable under stated assumptions

**Action:** Document each assumption clearly. Format: "Assuming [X], not [Y]. If [Y], estimate changes because [reason]."

### Kill

Feature should not be built. Recommend removing from scope.

**Indicators:**

- Not needed for the stated goal (nice-to-have, not must-have)
- Cost vastly exceeds value
- Duplicates functionality that already exists
- Premature — depends on other work that isn't planned yet
- Better solved by a different approach entirely

**Action:** Document the reason for killing. Be specific: "Killing because [reason]. Consider revisiting when [condition]."

### Split

Multiple features hiding under one label. Decompose into sub-features, then re-triage each.

**Indicators:**

- Feature description contains "and" connecting unrelated capabilities
- Multiple user types would use it differently
- Implementation naturally breaks into independent deliverables
- Could be partially shipped without the rest

**Action:** List the sub-features, re-triage each independently.

## Triage Questions Per Feature

Ask these for every feature during triage:

1. **Is this one feature or several?** Look for compound descriptions.
2. **Does the codebase already handle part of this?** Check architecture docs.
3. **Is this v1 or v2?** Is the client asking for the full vision or the minimum viable version?
4. **Who uses this?** Which user role, and is that role already in the system?
5. **What breaks without it?** Is this blocking other features or a standalone improvement?
6. **Is this the right solution?** Sometimes the feature label hides a problem that has a simpler solution.

## Triage Output Format

| Feature | Classification                                | Assumptions | Dependencies | Notes    |
| ------- | --------------------------------------------- | ----------- | ------------ | -------- |
| [name]  | scope / scope-with-assumptions / kill / split | [if any]    | [if any]     | [if any] |
