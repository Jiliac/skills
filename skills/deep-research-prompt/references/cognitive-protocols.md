# Cognitive Protocols for Deep Research Prompts

Three protocols that prevent the most common failure modes of autonomous research agents.

## 1. Data Triangulation

**Problem**: Agent finds one number and presents it as fact. Single-source metrics are unreliable due to reporting errors, corporate spin, or regional variance.

**Implementation**:

```
Do not accept a single source for any quantitative figure.
Find at least 3 independent sources for all market size numbers and financial metrics.
Cross-reference these sources, explicitly cite all three, and present the established range rather than a single static number.
```

**Why it works**: Neutralizes isolated reporting errors, biased press releases, and anomalous data points. Forces the agent to surface disagreement rather than hide it.

**Triangulation types to request**:

- Data triangulation: Same metric from multiple independent datasets
- Methodological triangulation: Same question approached via different methods (top-down market sizing vs. bottom-up)
- Source triangulation: Academic, government, and industry sources for the same claim

## 2. Devil's Advocate Protocol

**Problem**: Once the agent forms an initial hypothesis early in execution, its subsequent searches tend to confirm that hypothesis (confirmation bias). It constructs queries designed to corroborate, not challenge.

**Implementation**:

```
After generating your primary conclusion, dedicate a distinct section to "The Counter-Thesis."
Execute search queries designed specifically to find empirical evidence that disproves your main conclusion.
Present bear-case scenarios, liquidity traps, or execution bottlenecks BEFORE outlining upside drivers.
```

**Why it works**: Forces epistemic friction. The agent must actively retrieve and evaluate dissenting viewpoints, stress-testing its own conclusions. Produces balanced, risk-aware deliverables.

**Variations by domain**:

- Investment: "Present the bear case before the bull case"
- Technology: "Identify the top 3 reasons this technology could fail to achieve adoption"
- Strategy: "What would a well-funded competitor do to neutralize this advantage?"

## 3. Recursive Self-Correction

**Problem**: Agents formulate a preliminary answer and stop searching. Without explicit instruction, they don't review their own work for bias or logical gaps.

**Implementation**:

```
Before finalizing the report, review your own findings.
Identify any potential biases in your retrieved sources or logical gaps in your synthesis.
Attempt to resolve them with a mandatory second round of targeted, highly specific searching.
```

**Why it works**: Aligns with the Gödel Agent framework where models dynamically modify their own logic based on feedback. Without this step, the agent may reinforce incorrect assumptions. Recursive self-correction is the computational work required to maintain logical coherence.

**Key insight**: If a model cannot self-diagnose errors, giving it more compute time just produces more elaborate hallucinations. Self-correction must be explicitly activated.

## Combining All Three

For maximum rigor, chain the protocols in order:

1. **Triangulate** all quantitative claims (during research phase)
2. **Devil's Advocate** the primary conclusion (after synthesis)
3. **Self-correct** by reviewing for remaining bias and filling gaps (before output)

Example combined directive:

```
For every quantitative claim, find 3+ independent sources and present the range.
After forming your conclusion, write a Counter-Thesis section with evidence against it.
Before finalizing, self-review for source bias or logical gaps and run one more targeted search round to resolve them.
```
