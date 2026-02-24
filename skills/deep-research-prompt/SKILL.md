---
name: deep-research-prompt
description: Write structured prompts for agentic deep research tools (OpenAI Deep Research, Perplexity, Gemini, Manus AI). Use when the user wants to craft a research prompt, prepare a deep research mission, write a prompt for autonomous research agents, or optimize a research query for AI tools.
---

# Deep Research Prompt Writing

Write mission-briefing-style prompts that maximize output quality from autonomous deep research agents. These agents run independently for 5-30 minutes, execute hundreds of searches, and read thousands of pages. A vague prompt wastes massive compute and returns generic summaries.

The operator's mindset: you are a **strategic project manager deploying a digital analyst**, not a person typing a search query.

## Core Formula

Every deep research prompt must contain these six components:

```
Effective Prompt = Role + Objective + Context + Constraints + Safeguards + Format
```

## Step-by-Step Construction

### 1. Role & Audience

Define WHO the agent is and WHO reads the output. This forces the model into the right region of its latent space.

> Act as a Senior Strategy Consultant reporting to a board of directors.
> Tone: executive, data-driven, focused on ROI and strategic risk.

### 2. Mission Objective (Decision-Ready)

Frame the objective as a **decision to be made**, not a topic to explore. Use If-Then conditional logic to prevent open-ended drift.

> Decide whether [Company] should invest in [Technology] in 2026.
> If the technology is not projected to be commercially viable within 36 months, explicitly recommend "Wait."

Bad: "Tell me about solid state batteries."
Good: "Should we invest in solid state battery manufacturing? If unit costs won't drop below $X by 2028, recommend Hold."

### 3. Epistemic Constraints

Control **source quality**, **time window**, and **search depth**.

**Source hierarchy** (always specify):

> Prioritize peer-reviewed journals, official government datasets, and audited financial disclosures.
> Exclude SEO-spam blogs, promotional vendor materials, and unverified news outlets.

**Temporal bounds** (always specify):

> Focus on data published Q3 2024 to present. Flag anything older as "historical context" and do not use it in forward projections.

**Depth enforcement** (always specify):

> Do not stop at surface-level summaries. If Source A reports 10% growth and Source B reports 50%, investigate and explain the methodological divergence.

### 4. Cognitive Safeguards

Embed these three protocols to prevent hallucination, confirmation bias, and single-source risk.

**Data Triangulation**: "Find at least 3 independent sources for every quantitative claim. Present the range, not a single number."

**Devil's Advocate**: "After your main conclusion, dedicate a section to 'The Counter-Thesis.' Execute searches specifically designed to disprove your primary finding."

**Recursive Self-Correction**: "Before finalizing, review your own findings for source bias or logical gaps. Execute a second round of targeted searches to resolve them."

### 5. Output Architecture

Force rigid structure on the deliverable. Without this, agents produce impenetrable walls of text.

Always require these four sections:

1. **Executive Summary** - Max 1 page, Bottom Line Up Front (BLUF)
2. **Strategic Matrix** - Comparison table (options vs. cost, feasibility, risk, scalability)
3. **Confidence Assessment** - Low/Medium/High per major claim, based on source quality and volume
4. **Gap Analysis** - What the agent tried to find but could not verify; areas requiring human intelligence

## Prompt Template

```markdown
## Role

Act as [specific role]. The audience is [specific audience], so the tone should be [tone qualities].

## Objective

The mission is to determine whether [specific decision].

- If [condition A], recommend [action A].
- If [condition B], recommend [action B].

## Context

[2-3 sentences of background the agent needs to orient its search]

## Constraints

- **Sources**: Prioritize [source types]. Exclude [source types].
- **Time window**: Focus on [date range]. Flag older data as historical context only.
- **Depth**: Do not accept surface-level answers. Investigate contradictions between sources.
- **Triangulation**: Find 3+ independent sources for every quantitative claim.

## Cognitive Protocols

- After forming your primary conclusion, write a "Counter-Thesis" section with evidence against it.
- Before finalizing, self-review for bias or gaps and run a second search round.

## Output Format

1. **Executive Summary** (1 page max, BLUF methodology)
2. **Strategic Comparison Matrix** (table comparing options on [variables])
3. **Confidence Scores** (Low/Medium/High per claim)
4. **Gap Analysis** (what you could not verify)
5. **Sources** (full citations, grouped by section)
```

## Platform Selection Guide

| Platform                 | Best For                                                               | Speed    |
| ------------------------ | ---------------------------------------------------------------------- | -------- |
| OpenAI Deep Research     | Exhaustive synthesis, complex reasoning, executive reports             | 5-30 min |
| Perplexity Deep Research | Time-sensitive market intelligence, fact-checking, source transparency | ~3 min   |
| Manus AI                 | Multi-day workflows, continuous monitoring, offline execution          | Async    |
| Google Gemini Deep Think | Massive data ingestion, multimodal synthesis, expert-level problems    | Variable |

## References

- **Advanced cognitive protocols**: See [references/cognitive-protocols.md](references/cognitive-protocols.md) for detailed Devil's Advocate, Triangulation, and Self-Correction techniques
- **Platform deep-dive**: See [references/platform-comparison.md](references/platform-comparison.md) for architectural details on each research platform
- **Examples**: See [references/examples.md](references/examples.md) for complete prompt examples across domains
