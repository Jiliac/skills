# LLM-Era Estimation Model

## Core Insight: What Takes Time Has Changed

With LLM-assisted development (Claude Code, Cursor, etc.), the bottleneck has shifted fundamentally:

**What is fast now (minutes to hours):**

- CRUD operations, migrations, schema changes
- Validation logic, form scaffolding
- Service layer functions wrapping database queries
- RLS policies following established patterns
- Feature flags, routing, component boilerplate
- UI components following existing patterns (data tables, cards, forms)
- TypeScript types, interfaces, barrel exports
- Test scaffolding for deterministic logic

**What still takes real time (hours to days):**

- R&D where the outcome is uncertain (algorithm design, calibration, prompt engineering)
- External API integration with unknown behavior, latency, or reliability
- Complex state synchronization (real-time, multi-agent, WebSocket)
- Architectural novelty — patterns that don't exist in the codebase yet
- Integration points where the seam between systems is unclear
- LLM prompt iteration when output quality is unpredictable
- Product decisions that block implementation (conflict resolution rules, threshold values)
- Debugging non-deterministic behavior (AI outputs, race conditions, vendor API quirks)

**The rule of thumb:** If the spec is clear and the patterns exist, the code writes itself in minutes regardless of volume. A 500-line migration with 4 tables, RLS policies, and indexes is 15 minutes of work. A 20-line function calling an unfamiliar external API with unclear error semantics is 2 days. **Estimate based on uncertainty, not code volume.**

## Cost Structure Per Story

| Component                                                           | Time               | Predictability             |
| ------------------------------------------------------------------- | ------------------ | -------------------------- |
| **Spec writing** (architecture decisions, FRs, success criteria)    | ~2hrs fixed        | High — always needed       |
| **Deterministic code** (CRUD, migrations, UI, validation, services) | ~minutes           | High — LLM handles this    |
| **R&D / integration / debug**                                       | 0hrs to many hours | Low — this is the variance |

## The Fixed Cost

Every story has a ~2hr fixed cost (~0.25 days) for writing specs good enough that the LLM can execute correctly. This includes:

- Defining what needs to change and how
- Stating assumptions explicitly
- Writing verifiable success criteria
- Reviewing the LLM's plan before execution

## Where Estimates Should Be Concentrated

When decomposing a feature into sub-tasks, **do not allocate meaningful time to well-specified CRUD work.** Instead, concentrate estimate days on:

1. **Unknowns:** External APIs, new vendor integrations, novel patterns
2. **R&D iteration:** Algorithm design, threshold calibration, prompt engineering
3. **Integration seams:** Where two systems meet and behavior is not fully specified
4. **Product decision dependencies:** Specs blocked on decisions from stakeholders
5. **Calibration loops:** Features that need tuning against real data (scoring thresholds, difficulty tiers, detection sensitivity)

A feature with 8 sub-tasks where 6 are CRUD and 2 are R&D should be estimated almost entirely based on the 2 R&D tasks. The 6 CRUD tasks combined might be half a day.

## Debug Risk Levels

Debug risk is the primary variable in LLM-era estimation. It reflects **uncertainty**, not **volume**.

### Low Risk (+0-25%)

- Well-understood patterns already in the codebase
- Pure CRUD, configuration, UI following existing component patterns
- No external dependencies, no AI/LLM calls
- Clear, unambiguous requirements with established implementation path
- _Example: new database table + service + dashboard card following existing patterns_

### Medium Risk (+25-75%)

- New patterns within a known framework
- Integration with well-documented external APIs
- Product decisions needed but bounded (threshold values, UX choices)
- Moderate edge cases, some state management complexity
- _Example: new scoring dimension, cohort aggregation on JSONB fields, admin UI with new visual patterns_

### High Risk (+75-200%)

- Architectural novelty (new subsystem, new real-time protocol)
- External API with unknown behavior, latency, or reliability
- R&D nature — outcome depends on empirical data that doesn't exist yet
- LLM prompt engineering where output quality is unpredictable
- Multi-system state synchronization (voice + text + scoring pipelines)
- _Example: Gemini audio analysis integration, adaptive difficulty calibration, real-time coaching detection_

## Estimate Range Formula

- **Optimistic:** Spec cost + deterministic code (fast). All unknowns resolve cleanly on first try.
- **Expected:** Spec cost + code + one iteration cycle on each R&D unknown. Normal friction.
- **Pessimistic:** Spec cost + code + multiple iteration cycles. Unknowns materialize, vendor issues, rework needed.

**Range width signals risk:** A 4/5/7 range means low risk. A 5/7/12 range means real R&D uncertainty. If the optimistic and pessimistic are more than 2.5x apart, the feature has genuine unknowns that should be called out.

## Debug Risk Triggers

When analyzing a feature, flag these as debug risk elevators:

- First time using a pattern in this codebase
- Integration with external services (APIs, webhooks, OAuth)
- Real-time features (WebSocket, SSE, voice streaming)
- AI/LLM integration where output consistency matters
- Calibration against data that doesn't exist yet
- Complex state management across multiple systems
- Features touching the critical path (scoring, chat, session management)
- Vendor lock-in concerns (single-provider dependency)

**Not debug risk elevators** (these are fast with LLM-assisted dev):

- Large number of database tables or columns
- Many CRUD endpoints or service functions
- Complex but well-specified UI (forms, tables, charts)
- RLS policies following established patterns
- Feature flags, routing, permission checks
- Migration files, type generation, barrel exports

## Presenting Estimates to Clients

- Show the range: "3-5 days" not "4 days"
- Debug risk is internal — don't surface "high debug risk" to the client
- The risk is baked into the range width (tight range = low risk, wide range = high risk)
- For high-risk features, explain the uncertainty driver: "5 days expected, up to 8 if [specific unknown] is more complex than anticipated"
- Never estimate based on lines of code or number of files — estimate based on number of unknowns and iteration cycles
