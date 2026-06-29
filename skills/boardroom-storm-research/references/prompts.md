# Boardroom STORM — the nine prompts

Run in order. Replace bracketed text. Use web search / research mode when current facts matter. Show each stage's output to the user before continuing.

---

## Prompt 0 — Research charter

You are going to run Boardroom STORM, an adaptation of Stanford STORM: Synthesis of Topic Outlines through Retrieval and Multi-perspective Question Asking.

Topic: [TOPIC]
Decision context: [What decision, thesis, memo, article, or strategy this research will inform]
Primary audience: [Founder / investor / builder / board / product team / analyst readership]
Time horizon: [e.g., current state, next 12 months, 3-5 years]
Geography or segment: [if relevant]
Source hierarchy: prioritize [primary filings, company docs, technical docs, academic papers, regulatory docs, reputable journalism, expert blogs, podcasts, etc.]
Output target: [investment memo / market map / competitive analysis / product strategy / long-form article / board memo]

Rules:

1. Separate research from writing.
2. Do not draft the final piece until the source ledger, interview briefs, contradiction map, and outline are complete.
3. Cite sources for factual claims when web/research tools are available.
4. If a claim cannot be verified, mark it as Unverified rather than smoothing over it.
5. Maintain an uncertainty ledger with weak claims, stale sources, contradictions, and missing data.

First, restate the research charter in 8 bullets and identify any assumptions you will make.

---

## Prompt 1 — Perspective discovery

Run the Perspective Discovery stage.

Generate 8-10 distinct research perspectives for [TOPIC]. Do not use generic labels only. Each perspective should represent a real decision lens that would ask different questions.

Required perspectives to consider:

- Practitioner/operator who deals with this daily
- Customer/user or buyer
- Incumbent competitor
- Startup challenger
- Regulator or policy expert
- Economist/business model analyst
- Technical architect or engineer
- Skeptic/bear-case analyst
- Historian/comparable-cycles analyst
- Investor/capital allocator

For each perspective, provide:

1. Persona name
2. Why this lens matters for the decision
3. What this persona knows that others miss
4. 5 sharp questions this persona would ask
5. 3 likely source types this persona would trust
6. One blind spot this persona is likely to have

End with a ranked list of the 12 highest-leverage questions across all perspectives.

---

## Prompt 2 — Source scout and retrieval plan

Run the Source Scout stage for [TOPIC].

Using the perspective list above, build a source plan before answering the research questions.

For each perspective:

1. List the exact queries you would run or source categories you would inspect.
2. Identify the most authoritative source types for that perspective.
3. State what evidence would confirm, weaken, or falsify that perspective's likely thesis.

Then, if web/research tools are available, gather sources and create a source ledger with:

- Source title
- URL
- Publisher/author
- Date
- Perspective(s) it informs
- Key claims or data points
- Credibility rating: High / Medium / Low
- Freshness rating: Current / Potentially stale / Historical
- Notes on bias or limitations

Do not synthesize yet. Return the source ledger first.

---

## Prompt 3 — Multi-perspective simulated expert interviews

Run the Simulated Expert Interview stage.

For each perspective, simulate a 6-turn interview between:

- Interviewer: a rigorous analyst trying to understand [TOPIC]
- Expert: the persona for that perspective, grounded only in the source ledger and clearly marked assumptions

Interview rules:

1. The interviewer asks one question at a time.
2. Each follow-up must build on the previous answer.
3. The expert must cite the relevant source from the ledger for factual claims, or say Unverified.
4. The expert must distinguish facts, interpretations, and implications.
5. The final answer from each expert must include: strongest claim, weakest claim, what would change their mind, and the one question nobody else is asking.

Output format:

- Perspective name
- 6 Q&A turns
- Evidence table
- Claims to carry forward
- Claims to discard or verify later

---

## Prompt 4 — Contradiction map and unknown-unknowns pass

Run the Contradiction Map stage.

Using the interview briefs and source ledger, identify:

1. Direct contradictions: where two perspectives make incompatible claims.
2. Evidence asymmetries: where one side has stronger evidence than another.
3. Incentive conflicts: who benefits if a given interpretation becomes accepted.
4. Timing conflicts: what may be true now but false in 12-24 months.
5. Definition conflicts: where people use the same words to mean different things.
6. Missing perspectives: who was not represented and why that could matter.
7. Unknown unknowns: questions that emerged only because the perspectives interacted.

Create a table with columns:

- Issue
- Perspectives in conflict
- Claim A
- Claim B
- Evidence strength
- What would resolve it
- Decision implication

End with:

- What all perspectives agree on
- What nobody adequately addressed
- The 5 facts most likely to change the conclusion

---

## Prompt 5 — Outline synthesis

Run the Outline Synthesis stage.

Create a source-mapped outline for [OUTPUT TARGET] on [TOPIC].

Requirements:

1. Start with the decision the reader needs to make.
2. Organize sections by logic, not by the order sources were found.
3. For each section, list the claims it will make and the sources that support each claim.
4. Include a section for contradictions and open questions.
5. Include a section for implications by persona: founder, entrepreneur/operator, builder/product leader, investor.
6. Do not write prose yet except for section descriptions.

Output:

- Working title
- One-sentence thesis
- Reader promise
- Detailed hierarchical outline
- Source map by section
- Claims excluded because evidence is weak
- Open questions to verify before drafting

---

## Prompt 6 — Grounded drafting

Draft the [OUTPUT TARGET] from the approved outline.

Rules:

1. Use only the source-mapped outline, source ledger, interview briefs, and contradiction map.
2. Every factual claim needs an inline citation when citations are available.
3. Do not hide uncertainty; name it precisely.
4. Write for [AUDIENCE] with an investor-grade, practical tone.
5. Include concrete implications for founders, entrepreneurs/operators, builders, and investors.
6. Prefer tables where comparison matters.
7. Avoid generic AI prose: no vague "transformative," "game-changing," or "rapidly evolving" unless the evidence justifies it.

Structure:

- Executive thesis
- Why now
- What the evidence says
- Contradictions and open questions
- Persona-specific implications
- Action checklist
- Final decision memo / conclusion

---

## Prompt 7 — Co-STORM moderator refinement

Run a Co-STORM-style Moderator Pass on the draft.

Act as a skeptical moderator whose job is to find unknown unknowns, source bias, weak reasoning, and decision risks.

Review the draft for:

1. Missing stakeholder perspective
2. Overweighted source cluster
3. Unsupported causal claim
4. Over-association of unrelated facts
5. Stale or geography-specific evidence presented too broadly
6. Incentive misread
7. Technical feasibility gap
8. Regulatory or compliance blind spot
9. Competitive response not considered
10. Investor-relevant downside case

Return:

- 10 required fixes ranked by importance
- A revised thesis if needed
- A revised outline if needed
- Confidence scores for the 10 most important claims
- A final uncertainty ledger
- The 5 diligence questions a serious investor or board member would ask next

---

## Prompt 8 — Finalization

Produce the final version.

Incorporate the moderator fixes. Preserve nuance, citations, and uncertainty. Add:

1. A one-page executive memo at the top.
2. A persona-specific action table for founders, entrepreneurs/operators, builders, and investors.
3. A "what would change this conclusion" section.
4. A "next 7 days" action plan.
5. A clean source and claim audit table if citations are available.

Before finalizing, confirm that:

- The draft answers the original decision context.
- No major claim lacks support or a caveat.
- Contradictions are explicit rather than buried.
- The conclusion is actionable, not just informative.
