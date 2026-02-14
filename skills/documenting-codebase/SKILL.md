---
name: documenting-codebase
description: Generate comprehensive codebase documentation from source code. Creates a docs/ folder with a master architecture overview and 8-12 area docs written in parallel. Use when asked to document a codebase, generate technical documentation, create architecture docs, write a docs folder, or replace outdated documentation.
---

# Codebase Documentation Generator

Generate a complete, source-code-verified documentation suite for any codebase. The output is a `docs/` folder with a master architecture file, 8-12 area docs, and an optional legacy audit.

## 6-Phase Workflow

### Phase 1: Reconnaissance

Read key entry points to understand the codebase shape:

- Entry files (main, app, index)
- Package manifest (package.json, Cargo.toml, go.mod, etc.)
- Config files (build, deploy, CI)
- Existing README and docs
- Directory listing of `src/` (or equivalent)

Output: mental model of tech stack, directory structure, data flow, and logical areas.

### Phase 2: Master Architecture File

Write `docs/00-ARCHITECTURE.md` covering:

- What the project is (3 sentences)
- Tech stack table
- Annotated directory map
- End-to-end data flow diagram (ASCII)
- Summary table of N areas (2-3 sentences each + key files + doc link)
- Key architectural patterns
- Key decisions and legacy notes

Template: see [references/master-template.md](references/master-template.md)

### Phase 3: Area Docs (Parallel)

Break the codebase into 8-12 logical areas. Spawn one sub-agent per area, all in parallel. Each agent:

1. Reads ALL relevant source files (not just headers)
2. Writes one doc following the area template
3. Keeps under 400 lines
4. Uses `file:line` code references

Template: see [references/area-template.md](references/area-template.md)

**Sub-agent prompt pattern:**

```
Write `docs/{NN}-{area-name}.md` (max 400 lines).
[What the project is -- 1 sentence]
[Template sections to follow]
[Files to read -- list ALL explicitly]
[What to cover -- specific bullet points]
Write to: /absolute/path/docs/{NN}-{area-name}.md
```

Use `subagent_type: "general-purpose"` with `mode: "bypassPermissions"` and `run_in_background: true`.

### Phase 4: Cross-Reference Update

After all area docs complete:

1. Read all area docs to collect actual `##` section headers
2. Update `00-ARCHITECTURE.md`:
   - Fill cross-references table (concept -> doc -> exact section header)
   - Update area summary table with accurate descriptions
   - Add quick navigation links
   - Remove placeholder notes
3. Verify: confirm every link in `00-ARCHITECTURE.md` points to an existing file, every cross-reference section header exists in its target doc, and no placeholder text (`TODO`, `TBD`) remains.

### Phase 5: Legacy Audit (if existing docs exist)

Read every file in existing docs folder. Write `docs/LEGACY_DOCS_AUDIT.md` classifying each as:

- **CURRENT**: Accurate, not covered by new docs. Keep.
- **OUTDATED**: References old versions. Needs update/removal.
- **SUPERSEDED**: Fully covered by a new area doc. Safe to delete.
- **ARCHIVE**: Historical value (ADRs, changelogs). Keep for context.

Output as: `| File | Status | Replacement | Notes |`

### Phase 6: Folder Reorganization (if legacy docs exist)

Reorganize so current docs are immediately visible:

```
docs/
├── 00-ARCHITECTURE.md          # Entry point
├── 01- through NN-*.md         # Area docs
├── guides/                     # Operational/dev how-to docs (CURRENT)
├── adr/                        # Architecture Decision Records (ARCHIVE)
└── _legacy/                    # Superseded + outdated (historical reference)
    └── README.md               # Explains what's here
```

Use `git mv` for tracked files. Update all internal links. Remove stale references.

## Choosing Areas

Split by domain boundaries, not file types. Good areas: "Authentication", "Scoring Pipeline", "Chat Flow", "Brand Management". Bad areas: "Components", "Hooks", "Utils".

Each area should have:

- A clear purpose (one sentence)
- 5-30 key source files
- Identifiable data flow
- Minimal overlap with other areas

## Key Rules

- Read source code, not just existing docs -- existing docs may be wrong
- Every claim must be verifiable against code
- Max 400 lines per area doc, ~350 lines for master
- Use `file:line` references for key code locations
- Parallel sub-agents for area docs (massive time savings)
- Cross-references must use exact `##` headers from target docs

## References

- [references/master-template.md](references/master-template.md) -- Template for 00-ARCHITECTURE.md
- [references/area-template.md](references/area-template.md) -- Template for area docs
- [references/area-splitting-guide.md](references/area-splitting-guide.md) -- How to identify areas by stack type
