# Platform Comparison for Deep Research

Architectural details and prompt-tuning guidance for each major research platform.

## OpenAI Deep Research (GPT-5 series)

- **Architecture**: GPT-5.2 / GPT-5.3-Codex-Spark (128k context)
- **Execution window**: 5-30 minutes autonomous operation
- **Strengths**: Exhaustive depth, structural synthesis, complex memory retention, nuanced reasoning
- **Best for**: Academic literature reviews, technical engineering analysis, executive reporting
- **Benchmark**: 26.6% on Humanity's Last Exam (2x prior models)
- **Self-correction**: 88.9% improvement between first and second attempt after feedback (AgencyBench)
- **Enterprise**: Slack connectors, role-based access controls, proprietary data ingestion

**Prompt tips for OpenAI**:

- Lean into complex output structures (it excels at maintaining format over long outputs)
- Explicitly request recursive reasoning passes
- Use for missions requiring deductive chains across 10+ sources

## Perplexity Deep Research (DeepSeek R1 + TTC)

- **Architecture**: Customized DeepSeek R1 on proprietary Test-Time Compute framework
- **Execution window**: ~3 minutes
- **Strengths**: Speed, strict source traceability, factual grounding, transparency
- **Best for**: Time-sensitive market analysis, rapid corporate intelligence, fact-checking
- **Benchmark**: 21.1% on Humanity's Last Exam

**Prompt tips for Perplexity**:

- Favor speed-sensitive missions where 80% depth in 3 minutes beats 95% depth in 25 minutes
- Source citations are native; request explicit source comparison tables
- Best for prompts where traceability matters more than synthesis depth

## Google Gemini (3.1 Pro / Deep Think)

- **Architecture**: Large context window + Deep Think capabilities
- **Strengths**: Benchmark performance, multimodal comprehension, ecosystem integration
- **Best for**: Enterprise-scale data ingestion, multimodal synthesis, expert-level problems
- **Benchmark**: 44.7% on Humanity's Last Exam (highest recorded)
- **Self-correction**: 33.3% improvement on feedback (good initial intuition, weaker at pivoting)

**Prompt tips for Gemini**:

- Leverage multimodal: include charts, diagrams, images in the prompt context
- Best when feeding large document sets for in-context synthesis
- Strong initial answers but less adaptive; front-load constraints carefully

## Manus AI

- **Architecture**: Asynchronous cloud-based virtual environment
- **Execution window**: Continuous / async (runs while you're offline)
- **Strengths**: Persistent execution, tool utilization, multi-day workflows, offline operation
- **Best for**: Complex multi-day pipelines, continuous monitoring, tasks requiring software interaction

**Prompt tips for Manus**:

- Structure prompts as multi-phase missions with explicit checkpoints
- Define what "done" looks like at each phase
- Include fallback instructions for when the agent hits dead ends

## Choosing a Platform

| Need                          | Platform                            |
| ----------------------------- | ----------------------------------- |
| Maximum analytical depth      | OpenAI Deep Research                |
| Speed and source transparency | Perplexity                          |
| Multimodal or massive data    | Gemini                              |
| Multi-day autonomous work     | Manus AI                            |
| Self-correction capability    | OpenAI (best) > Gemini > Perplexity |
