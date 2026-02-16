# Argument/Thesis Post Frameworks

Detailed framework library for LinkedIn posts that make a case. The primary framework (CEIR) is in the main skill file. These are alternatives for when the content calls for a different structure.

---

## 1. CEIR — Claim, Evidence, Implication, Reframe

**Primary framework.** See main SKILL.md.

Best for: thesis posts, contrarian takes, industry analysis.
Examples: Posts 01 (Debugging), 03 (Nobody Knows), 07 (Building AI is R&D).

---

## 2. SCQA — Situation, Complication, Question, Answer

From Barbara Minto's _The Pyramid Principle_. Best for B2B tech posts where you need to earn the right to give advice.

```
1. SITUATION (1-2 lines)
   Shared reality. Something the reader knows and agrees with.
   "Every enterprise wants AI in production. Most have 3-5 pilots."

2. COMPLICATION (2-3 lines)
   What's wrong or what changed. Tension enters here.
   "But 87% of those pilots never make it past demo. The gap
   isn't technology — it's that nobody owns the production path."

3. QUESTION (implicit or explicit, 1 line)
   The question now in the reader's mind.
   "So how do you actually get from pilot to production?"

4. ANSWER (bulk of the post)
   Your thesis with evidence. 3-5 concrete points.
```

Best for: posts where you're diagnosing a systemic problem.

---

## 3. TAS — Thesis, Antithesis, Synthesis

Classical dialectic. Best for intellectual posts where you want to show you've considered both sides.

```
1. THESIS (your opening)
   The prevailing wisdom or initial position.
   "The AI industry says: ship fast, iterate later."

2. ANTITHESIS (the counterpoint)
   What contradicts the thesis. Use evidence.
   "But every production AI system I've built says the opposite.
   Governance on day 1 saves 6 months of rework."

3. SYNTHESIS (the higher truth)
   Resolve the tension into a more nuanced position.
   "Speed and governance aren't opposites. The fastest teams
   ship fast *because* they have constraints, not despite them."
```

Best for: industry analysis, nuanced takes where the truth is in the middle.

---

## 4. HTOF — Hot Take Opinion Framework

For strong contrarian takes that need to be earned through the post.

```
1. THE TAKE (1 line)
   Debatable position stated as fact. Not "unpopular opinion:" (overused).
   "RAG is a solved problem. The bottleneck is evaluation."

2. THE "HERE'S WHY" (3-5 points)
   Each backed by data, experience, or first-principles reasoning.
   2 sentences max per point. Numbered or line-broken.

3. THE STEEL MAN (1-2 lines)
   Acknowledge the strongest opposing argument.
   "I get it — retrieval quality still matters. But it's table stakes,
   not the frontier."

4. THE REFRAME (1-2 lines)
   Restate your take with the nuance you've built.

5. THE OPEN (1 line)
   Invite disagreement with a specific question.
   "What's the actual bottleneck in your RAG pipeline right now?"
```

The steel man is what separates practitioner posts from motivational-poster posts. It signals intellectual honesty.

Best for: strong opinions where you want substantive comments and debate.

---

## 5. Blame-Flip Roadmap

For contrarian posts that deliver hard truths without alienating the reader.

```
1. THE VICTIM SETUP
   Name a common failure. Blame the system, not the person.
   "Most engineers learn system design backwards."
   The reader is the victim. The villain is conventional wisdom.

2. THE REAL VILLAIN
   Why the default approach fails. Be specific.
   "Textbooks teach you to design for scale on day one.
   But 90% of systems never reach the scale they were designed for."
   This creates relief: "I'm not failing — I was failed."

3. THE ROADMAP
   The alternative path, concretely. 3-5 actionable steps.
   Without this, you're just another critic.
```

Best for: posts about broken industry defaults, wrong mental models.

---

## 6. PAS — Problem, Agitate, Solve (Opinion Variant)

Classic copywriting formula adapted for thesis-driven content.

```
1. PROBLEM (1-2 lines)
   Name a specific pain. Use "you" language.
   "Your AI demo worked perfectly. Your production deployment failed."

2. AGITATE (3-4 lines)
   Make the problem worse. Cascading consequences with specifics.
   "Now you're 3 months past deadline. The board is asking why.
   Your best ML engineer just quit because they're tired of
   babysitting a system that was never designed for production."

3. SOLVE → REFRAME (the thesis)
   Not a product pitch — your intellectual position.
   "The problem isn't your team. It's that demo-to-production
   requires a completely different architecture."
```

Replace "Solve" with "Reframe" — you're offering a new way to think, not selling.

Best for: posts about common failures, especially when you have a clear alternative.

---

## 7. Jasmin Alic Hook-Rehook-Body-Close

Focused on the mechanical architecture of how LinkedIn posts are read (mobile, "see more" fold).

```
1. HOOK (1 line, under ~150 characters)
   Your claim, compressed. Only thing visible before "see more."

2. REHOOK (1-2 lines)
   Crush the main objection OR add an unexpected angle.
   "And that means most companies are hiring wrong."
   [empty line — visual breathing room]

3. BODY (4-8 short paragraphs)
   Evidence, proof points, examples. 1-3 sentences per paragraph.
   Line breaks aggressively. Mobile readers scroll, not parse.

4. CLOSE (1-2 lines)
   Restate claim reframed, or provocative question.
```

Key data: hooks longer than 1 line perform 20% worse. Hooks with negative framing ("don't," "stop," "never") perform 30% worse. Lead with the positive reframe, not the negation.

Best for: any argument post — this is more about the mechanics than the intellectual structure. Can be layered on top of any other framework.

---

## Progressive Tension in Arguments

Across all frameworks, the tension pattern for arguments:

1. **Open with certainty** — state something boldly (opposite of story tension)
2. **Introduce the gap** — conventional approach vs. what actually works
3. **Escalate stakes** — concrete business consequences (cost, time, risk)
4. **Resolve with higher frame** — new mental model, not "winning the argument"

**Key difference from narrative tension:** Argument tension comes from cognitive dissonance (reader believed X, you show evidence for Y), not from "what happens next."

---

## Choosing a Framework

| Your content is...                            | Use         | Why                                  |
| --------------------------------------------- | ----------- | ------------------------------------ |
| A contrarian take backed by your experience   | CEIR        | Direct, matches your strongest posts |
| Diagnosing a systemic industry problem        | SCQA        | Earns the right to advise            |
| A nuanced position with two valid sides       | TAS         | Shows intellectual depth             |
| A strong opinion you want debated             | HTOF        | Steel man invites quality comments   |
| Calling out a broken default                  | Blame-Flip  | Reader is victim, not villain        |
| Describing a specific pain + your alternative | PAS-opinion | Emotional resonance                  |
| Any of the above (mechanical layer)           | Jasmin Alic | Hook/rehook structure on top         |

---

## Sources

- [Letterdrop - LinkedIn Thought Leadership](https://letterdrop.com/blog/linkedin-thought-leadership)
- [Autoposting.ai - LinkedIn Content Frameworks](https://autoposting.ai/linkedin-content-frameworks/)
- [Tech Audience Accelerator - Blame-Flip Roadmap](https://techaudienceaccelerator.substack.com/p/the-blame-flip-roadmap-prompt)
- [Natasha Musa - Lessons from Jasmin Alic](https://www.natashamusa.com/mastering-the-linkedin-post-key-lessons-from/)
- [Buffer - Copywriting Formulas](https://buffer.com/resources/copywriting-formulas/)
- [SlideModel - SCQA Framework Guide](https://slidemodel.com/scqa-framework-guide/)
- [Kleo - LinkedIn Post Templates](https://kleo.so/blog/linkedin-post-templates)
- [Copyblogger - 50 LinkedIn Post Templates](https://copyblogger.com/linkedin-post-templates/)
