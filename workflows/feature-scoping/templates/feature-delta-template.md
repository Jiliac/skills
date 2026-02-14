---
feature_name: ""
status: ""
date: ""
estimate_optimistic: 0
estimate_expected: 0
estimate_pessimistic: 0
debug_risk: ""
dependencies: []
---

# Feature: {{feature_name}}

## Purpose

<!-- One-sentence: what problem does this solve for which user -->

## Functional Requirements

<!-- Copied from main report for reference -->

## Architecture Delta

### What Exists

<!-- Existing services, endpoints, UI components, DB tables that already handle part of this -->

### What Needs Extending

<!-- Existing code that needs modification. Note complexity: trivial / moderate / significant -->

### What's New

<!-- Entirely new modules, services, patterns. Flag architectural novelty -->

### Unknowns

<!-- External APIs to evaluate, libraries to research, design decisions needing prototyping -->

## Sub-Task Decomposition

<!-- At 0.5-day granularity -->

| #   | Sub-Task | Days | Notes |
| --- | -------- | ---- | ----- |

## Estimation

| Scenario    | Days | Rationale                 |
| ----------- | ---- | ------------------------- |
| Optimistic  |      | Clean execution, no debug |
| Expected    |      | Risk-adjusted             |
| Pessimistic |      | Unknowns materialize      |

**Debug Risk:** {{debug_risk}}
**Risk Factors:** <!-- What specifically could blow up the estimate -->

## Dependencies

<!-- Other features this depends on or that depend on this -->
