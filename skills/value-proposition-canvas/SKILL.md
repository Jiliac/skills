---
name: value-proposition-canvas
description: Guide for creating Value Proposition Canvases (Osterwalder/Strategyzer methodology). Use when designing, analyzing, or refining product-market fit, mapping customer needs to product features, or writing value propositions for landing pages, pitches, or App Store copy.
---

# Value Proposition Canvas

Structured framework by Alex Osterwalder (Strategyzer) to ensure product-customer fit. Two sides, one mapping exercise.

## When to Use

- Defining what to build before coding (feature prioritization)
- Writing landing page copy, App Store descriptions, pitch decks
- Evaluating product-market fit for an existing product
- Comparing your offer against competitors
- Preparing for user interviews (what to validate)

## Core Workflow

### Step 1: Pick One Customer Segment

One canvas per segment. Never mix segments on a single canvas.

### Step 2: Fill the Customer Profile (right side)

Map the customer's world _independent of your solution_:

1. **Jobs** - What they're trying to accomplish
2. **Pains** - What blocks or frustrates them
3. **Gains** - What would delight them or make life better

Rank each item by intensity (essential vs. nice-to-have, extreme vs. moderate).

See [references/customer-profile.md](references/customer-profile.md) for job types, pain/gain categories, and trigger questions.

### Step 3: Fill the Value Map (left side)

Map your offering:

1. **Products & Services** - Your actual features and deliverables
2. **Pain Relievers** - How each feature kills a specific pain
3. **Gain Creators** - How each feature creates a specific gain

See [references/value-map.md](references/value-map.md) for definitions and worked examples.

### Step 4: Map the Fit

Draw explicit connections between left and right:

- Every Pain Reliever connects to a specific Pain
- Every Gain Creator connects to a specific Gain
- **Unconnected features = cut candidates**
- **Unaddressed pains/gains = product gaps or deliberate scope choices**

### Step 5: Synthesize the Value Proposition Statement

> "For **[segment]** who **[key job/pain]**, **[product]** is a **[category]** that **[key benefit]** unlike **[alternative]** which **[limitation]**."

### Step 6: Validate and Iterate

The canvas is a hypothesis. Test with:

- Customer interviews (do these jobs/pains/gains resonate?)
- Landing page tests (does the statement convert?)
- Usage data (do features mapped as relievers actually reduce churn?)

See [references/fit-and-validation.md](references/fit-and-validation.md) for validation methods and fit levels.

## Output Format

When generating a Value Proposition Canvas, use this structure:

```markdown
# Value Proposition Canvas: [Product] x [Segment]

## Customer Profile

### Jobs

| Priority | Type       | Job |
| -------- | ---------- | --- |
| High     | Functional | ... |

### Pains

| Severity | Pain | Current Workaround |
| -------- | ---- | ------------------ |
| Extreme  | ...  | ...                |

### Gains

| Importance | Gain |
| ---------- | ---- |
| Essential  | ...  |

## Value Map

### Products & Services

- [Feature 1]
- [Feature 2]

### Pain Relievers

| Pain | Reliever | Feature |
| ---- | -------- | ------- |
| ...  | ...      | ...     |

### Gain Creators

| Gain | Creator | Feature |
| ---- | ------- | ------- |
| ...  | ...     | ...     |

## Fit Analysis

- Addressed pains: X/Y
- Addressed gains: X/Y
- Unconnected features: [list]
- Gaps: [list]

## Value Proposition Statement

> "For ... who ..., [Product] is a ... that ... unlike ... which ..."
```

## Critical Rules

1. **Always start with customer profile** - never start from your features
2. **Pains exist independently of your solution** - "lacks feature X" is not a pain
3. **One canvas per segment** - mixing segments produces noise
4. **Rank everything** - not all jobs/pains/gains are equal
5. **Map explicitly** - vague "it helps" connections don't count

## References

- [references/customer-profile.md](references/customer-profile.md) - Job types, pain/gain categories, trigger questions
- [references/value-map.md](references/value-map.md) - Products, pain relievers, gain creators with examples
- [references/fit-and-validation.md](references/fit-and-validation.md) - Fit levels, validation methods, iteration
- [references/common-mistakes.md](references/common-mistakes.md) - Pitfalls and how to avoid them
