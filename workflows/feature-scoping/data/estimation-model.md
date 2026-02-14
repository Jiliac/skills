# LLM-Era Estimation Model

## Cost Structure Per Story

| Component                                                                                           | Time               | Predictability             |
| --------------------------------------------------------------------------------------------------- | ------------------ | -------------------------- |
| **Spec writing** (architecture decisions, FRs, success criteria, Karpathy-style verification steps) | ~2hrs fixed        | High — always needed       |
| **Code generation** (LLM writes it)                                                                 | ~minutes           | High — fast                |
| **Debug/integration**                                                                               | 0hrs to many hours | Low — this is the variance |

## The Fixed Cost

Every story has a ~2hr fixed cost (~25% of a dev day) for writing specs good enough that the LLM can execute correctly. This includes:

- Defining what needs to change and how
- Stating assumptions explicitly
- Writing verifiable success criteria (Karpathy guidelines)
- Reviewing the LLM's plan before execution

## Debug Risk Levels

Debug risk is the primary variable in LLM-era estimation. It determines the padding applied to the base estimate.

### Low Risk

- Well-understood patterns already in the codebase
- Existing similar code to reference
- No external dependencies
- Clear, unambiguous requirements
- **Padding:** Minimal (+0-25%)

### Medium Risk

- New patterns within a known framework
- Moderate complexity, some edge cases
- Internal dependencies on other features
- Requirements clear but implementation path has options
- **Padding:** Moderate (+25-75%)

### High Risk

- Architectural novelty (new subsystem, new pattern)
- External API integration (unknown behavior, rate limits, auth)
- Unclear or ambiguous requirements (even with assumptions)
- Interaction with existing tech debt
- Cross-cutting concerns (auth, permissions, data migration)
- **Padding:** Significant (+75-200%)

## Estimate Range Formula

- **Optimistic:** Base spec cost + minimal implementation. Everything goes right, no debugging.
- **Expected:** Spec cost + implementation + debug risk padding. Normal friction applied.
- **Pessimistic:** Spec cost + implementation + worst-case debug. Unknowns materialize, rework needed.

## Debug Risk Triggers

When analyzing a feature, flag these as debug risk elevators:

- First time using a pattern in this codebase
- Integration with external services (APIs, webhooks, OAuth)
- Data migration or schema changes on populated tables
- Real-time features (WebSocket, SSE, polling)
- Complex state management across multiple components
- Permission/auth changes (RLS policies, role guards)
- Features touching the critical path (scoring, chat, payments)

## Presenting Estimates to Clients

- Show the range: "3-5 days" not "4 days"
- Debug risk is internal — don't surface "high debug risk" to the client
- Instead, the risk is baked into the range width (tight range = low risk, wide range = high risk)
- For high-risk features, offer: "5 days expected, up to 8 if [specific unknown] is more complex than anticipated"
