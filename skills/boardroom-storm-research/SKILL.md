---
name: boardroom-storm-research
description: Run decision-grade, multi-perspective research using Boardroom STORM (an adaptation of Stanford's STORM method). Use when the user wants a rigorous research report, market map, investment/diligence memo, competitive analysis, board memo, product strategy, or long-form thesis on an ambiguous topic where smart people would disagree — anything where a shallow consensus answer is costly. Triggers: "run Boardroom STORM", "STORM research", "research X thoroughly", "build a diligence/thesis/board memo", "map this market". Do NOT use for single factual lookups answerable with one or two web searches.
---

# Boardroom STORM

A six-stage research workflow that front-loads **organization** before writing: discover perspectives → scout sources → simulate expert interviews → map contradictions → outline → draft → moderator pass. Adapted from Stanford OVAL Lab's STORM (Synthesis of Topic Outlines through Retrieval and Multi-perspective Question Asking) and Co-STORM. The point is not prettier prose — it is finding the questions and contradictions a generic report misses.

## When to use

High when the cost of a shallow answer is high: entering a market, writing a public thesis, diligence on a startup, evaluating a protocol, mapping competitors, a board memo, or deciding if a trend is signal or noise. The sweet spot is an **ambiguous topic where five smart people would disagree before converging**. Skip it for a simple factual lookup — plain web search is better there.

## How to run it

1. **Gather the charter inputs first.** Ask the user (or infer and state) the bracketed fields in Prompt 0: topic, decision context, audience, time horizon, geography/segment, source hierarchy, output target. Do not skip this — it shapes every later stage.
2. **Enable retrieval.** Use web search / research mode whenever current facts matter. Every factual claim needs a citation, or it is marked `Unverified`.
3. **Run the nine prompts in order**, from `references/prompts.md`. Each prompt is one stage; substitute the bracketed values. Show the user the output of each stage and let them steer before continuing (this is the Co-STORM "human-in-the-loop" discipline). For an autonomous run, proceed stage to stage but still surface the source ledger, contradiction map, and outline as checkpoints.
4. **Hold the outline-before-draft line.** Do not write the final piece until the source ledger, interview briefs, contradiction map, and outline are all complete.

## The six stages (nine prompts)

| Stage                          | Prompt(s)       | Produces                                                   |
| ------------------------------ | --------------- | ---------------------------------------------------------- |
| 0. Charter                     | Prompt 0        | Restated charter + assumptions                             |
| 1. Perspectives                | Prompt 1        | 8–10 decision lenses + ranked top-12 questions             |
| 2. Source scout                | Prompt 2        | Source ledger (credibility + freshness rated)              |
| 3. Interviews                  | Prompt 3        | 6-turn simulated expert interview per perspective          |
| 4. Contradictions              | Prompt 4        | Contradiction map + unknown-unknowns + 5 conclusion-movers |
| 5. Outline                     | Prompt 5        | Source-mapped outline (no prose yet)                       |
| 6. Draft → moderate → finalize | Prompts 6, 7, 8 | Grounded draft → skeptical moderator pass → final memo     |

The full copy-paste text of all nine prompts is in `references/prompts.md`. Read it before starting and follow it stage by stage.

## Non-negotiable quality rules

- **Separate research from writing.** No drafting before the outline is source-mapped.
- **Never skip the source ledger.** STORM is retrieval + question-asking, not brainstorming with academic branding.
- **Never let one persona dominate.** Value comes from discourse among lenses, not a single authoritative voice.
- **Never hide uncertainty.** Maintain an uncertainty ledger (weak claims, stale sources, contradictions, missing data). Mark unverifiable claims `Unverified` rather than smoothing over them.
- **Never confuse confidence with evidence.** Inspect citations; the user decides if evidence is adequate for the decision.
- **Watch STORM's known failure modes** (flagged in the paper): source-bias transfer, and over-associating facts that merely co-occur. The moderator pass (Prompt 7) exists to catch these.

## What this is not

Not a replacement for Stanford's official STORM codebase, and not a substitute for expert diligence, legal/financial advice, customer calls, or technical validation. It is a better way to build the **first serious map** of a problem space and decide where human work should go next.

**Attribution:** Method adapted from Stanford OVAL Lab's STORM and Co-STORM research. Workflow framing ("Boardroom STORM") by Linas Beliūnas (Linas's Newsletter).
