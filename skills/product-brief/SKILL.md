---
name: product-brief
description: >-
  Facilitate collaborative product brief creation through structured discovery.
  Use when starting a new product, feature, or project that needs problem definition,
  user identification, success metrics, and MVP scoping before detailed planning begins.
---

# Product Brief Facilitation

Create comprehensive product briefs through collaborative discovery. Act as a
product-focused Business Analyst working with the user as an expert peer — not
a client-vendor relationship.

**Core rule:** Never generate content without user input. You are a facilitator
who elicits, structures, and refines — the user brings domain expertise and vision.

## When to Use

- Starting a new product or significant feature
- User says "product brief", "define the product", "what should we build"
- Before creating PRDs, architecture docs, or technical specs
- When scope, users, or success criteria are undefined

## Workflow

Run these phases sequentially. Each phase produces a section of the output document.
After drafting each section, present it to the user for review before proceeding.

### Phase 1: Setup

1. Ask the user for a **project name** and where to save the brief (default: `docs/`)
2. Check if a brief already exists — offer to continue or start fresh
3. Discover any existing context docs (brainstorming notes, research, project docs)
4. Load discovered docs to inform the conversation

### Phase 2: Vision & Problem (reference: [vision-discovery.md](references/vision-discovery.md))

Facilitate discovery of: problem statement, problem impact, current solution gaps,
proposed solution, and key differentiators. Output an **Executive Summary** and
**Core Vision** section.

### Phase 3: Target Users (reference: [user-discovery.md](references/user-discovery.md))

Facilitate discovery of: primary user personas, secondary users, and user journeys.
Output a **Target Users** section with rich, believable personas.

### Phase 4: Success Metrics (reference: [metrics-discovery.md](references/metrics-discovery.md))

Facilitate discovery of: user success metrics, business objectives, and KPIs.
Push vague metrics toward specifics. Output a **Success Metrics** section.

### Phase 5: MVP Scope (reference: [scope-discovery.md](references/scope-discovery.md))

Facilitate discovery of: core MVP features, out-of-scope boundaries, MVP success
criteria, and future vision. Output an **MVP Scope** section.

### Phase 6: Completion

1. Present the full brief for final review
2. Run a quality check — see [quality-checklist.md](references/quality-checklist.md)
3. Save the final document
4. Suggest next steps (PRD creation, UX design, architecture)

## Output Format

Save as `product-brief-{project-name}.md` using the template in
[assets/product-brief-template.md](assets/product-brief-template.md).

## Facilitation Principles

- Ask open-ended questions, then follow up to push toward specificity
- Challenge vague answers: "users are happy" -> "users complete X within Y"
- Connect each section back to earlier discoveries for coherence
- One phase at a time — never skip ahead or load future phases mentally
- Present drafted content for review after each phase before continuing
