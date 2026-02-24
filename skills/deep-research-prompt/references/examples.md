# Deep Research Prompt Examples

Complete prompt examples across different domains.

## Example 1: Technology Investment Decision

```markdown
## Role

Act as a Senior Strategy Consultant at a Tier-1 management consultancy.
The audience is the CEO and board of directors of a Fortune 500 automotive manufacturer.
Tone: executive, data-driven, focused on ROI and strategic risk.

## Objective

Determine whether the company should invest $500M in solid-state battery manufacturing capacity in 2026.

- If the technology is not projected to be commercially viable (unit cost below $120/kWh) within 36 months, recommend "Wait."
- If viable but competitive landscape is saturated (3+ major manufacturers at scale), recommend "Partner" over "Build."
- If viable and first-mover advantage exists, recommend "Invest."

## Context

The company currently sources lithium-ion cells from CATL and Samsung SDI. Board is concerned about supply chain concentration risk and EV margin pressure. Competitors Toyota and BMW have announced solid-state programs.

## Constraints

- Sources: Prioritize peer-reviewed journals (Nature Energy, Joule), IEA/DOE reports, and audited financial disclosures from public companies. Exclude promotional vendor materials and unverified news.
- Time window: Q3 2024 to present. Flag older data as historical context only.
- Depth: If sources disagree on cost projections, investigate the methodological differences (lab-scale vs. pilot-line vs. mass production assumptions).
- Triangulation: Find 3+ independent sources for all cost-per-kWh and market size figures.

## Cognitive Protocols

- After your primary recommendation, write a "Counter-Thesis" section presenting the strongest case for the opposite action.
- Before finalizing, self-review for source bias (e.g., over-reliance on bullish industry reports) and run a second search pass.

## Output Format

1. Executive Summary (1 page max, BLUF: state the recommendation in the first sentence)
2. Strategic Matrix (table: Build vs. Partner vs. Wait, scored on cost, timeline, risk, competitive position)
3. Confidence Scores (Low/Medium/High per major claim)
4. Counter-Thesis (strongest case against the recommendation)
5. Gap Analysis (what data was unavailable or unverifiable)
6. Sources (full citations grouped by section)
```

## Example 2: Market Entry Analysis

```markdown
## Role

Act as a market intelligence analyst at a B2B SaaS company.
The audience is the VP of Product and VP of Sales.
Tone: analytical, practical, focused on TAM sizing and competitive gaps.

## Objective

Determine whether the company should enter the Southeast Asian market for HR tech in 2026.

- If TAM is below $2B and growing less than 15% CAGR, recommend "Deprioritize."
- If TAM exceeds $2B but 3+ well-funded local competitors exist with >60% combined share, recommend "Acquire" over "Build."
- Otherwise, recommend "Enter" with a go-to-market sequence.

## Constraints

- Sources: Gartner, IDC, Statista, central bank reports from target countries (Singapore MAS, Indonesia OJK), and Series B+ funding announcements.
- Time window: 2024-present.
- Geography: Singapore, Indonesia, Philippines, Vietnam, Thailand.
- Triangulation: 3+ sources for any TAM figure. Present ranges, not point estimates.

## Cognitive Protocols

- Devil's Advocate: After your recommendation, present the case for why this market is a trap.
- Self-correction: Review whether your sources over-index on English-language reporting.

## Output Format

1. Executive Summary (BLUF)
2. Market Sizing Table (country x TAM x CAGR x competitive density)
3. Competitor Map (top 5 players per country, funding, market share)
4. Confidence Scores per country
5. Gap Analysis
6. Sources
```

## Example 3: Personal Life Decision

```markdown
## Role

Act as a research analyst helping an individual make a major career decision.
The audience is a non-technical person evaluating life options.
Tone: clear, honest, balanced. Avoid hype.

## Objective

Evaluate whether transitioning from corporate finance to AI/ML engineering is viable for a 32-year-old with no CS degree but strong quantitative skills.

- If median transition time exceeds 24 months AND expected salary is below current ($145K), recommend "Stay and upskill on the side."
- If viable paths exist under 12 months, recommend "Transition" with a specific learning roadmap.

## Constraints

- Sources: Bureau of Labor Statistics, LinkedIn Workforce Reports, credible bootcamp outcome reports (with audited placement rates, not marketing claims), and Hacker News salary threads.
- Exclude: Bootcamp marketing pages, paid advertorials, influencer content.
- Time window: 2024-present.
- Triangulation: 3+ sources for salary figures and job placement rates.

## Cognitive Protocols

- Devil's Advocate: After your recommendation, present the strongest case for why this transition would be a mistake.
- Self-correction: Review whether your sources skew toward survivorship bias (success stories over dropouts).

## Output Format

1. Bottom Line (1 paragraph decision)
2. Viable Pathways Table (path x duration x cost x expected outcome)
3. Risk Assessment (what could go wrong with each path)
4. Confidence Scores
5. Gap Analysis
6. Sources
```

## Anti-Pattern: What NOT to Write

Bad prompt (lazy ask):

```
Tell me about the electric vehicle market.
```

Why it fails:

- No role or audience: output defaults to generic Wikipedia-style overview
- No decision to make: agent has no stopping criterion
- No source constraints: agent mixes blog spam with research papers
- No output structure: produces an impenetrable wall of text
- No temporal bounds: mixes 2020 data with 2026 data
- No depth enforcement: agent stops at the first plausible answer
