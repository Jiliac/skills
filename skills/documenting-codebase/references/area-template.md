# Area Doc Template

Each area doc follows this structure. Adapt sections to the area -- skip sections that don't apply, add domain-specific sections as needed.

````markdown
# [Area Title]

> Part of [Project] docs. See [00-ARCHITECTURE.md](./00-ARCHITECTURE.md) for overview.

## Purpose

[2-3 sentences: what this area does, why it exists, key design philosophy]

## Key Files

| File              | Purpose             |
| ----------------- | ------------------- |
| `path/to/file.ts` | [Brief description] |
| ...               | ...                 |

## [Primary Content Sections]

[The meat of the doc. Structure depends on the area. Examples:]

### For a pipeline/flow area:

- Step-by-step pipeline with ASCII diagrams
- Input/output types at each step
- Where LLM vs deterministic logic is used

### For a UI/frontend area:

- Component tree or page structure
- State management approach
- Key hooks and their responsibilities
- Route access matrix

### For a data/database area:

- Table inventory grouped by domain
- Key relationships (ASCII ER diagram)
- Access control patterns (RLS, etc.)
- Migration organization

### For an API area:

- Endpoint registry (table: name, method, auth, description)
- Request/response patterns
- Error handling format
- Auth patterns

### For a config/admin area:

- Feature flags or config options
- Role-based access matrix
- Monitoring/alerting setup

## Data Flow

[ASCII diagram or numbered steps showing how data moves through this area]

\```
Input → Step 1 → Step 2 → Output
↓
Side effect
\```

## Key Patterns & Conventions

[Patterns specific to this area that a developer should know]

## Important Notes

[Gotchas, legacy decisions, things that look wrong but are intentional]

## Related Areas

- **[Area Name]**: see [NN-area-name.md](./NN-area-name.md) -- [why it's related]
- ...
````

## Guidelines

- Max 400 lines (target 350-380 for breathing room)
- Read ALL listed source files before writing -- don't guess from file names
- Use `file:line` references for key code locations (e.g., `scoring-config.ts:42`)
- Include actual type names, function names, and constants from the code
- ASCII diagrams for data flows (keep under 10 lines)
- Tables for inventories (files, endpoints, config options)
- Cross-reference related area docs in the Related Areas section
- Don't duplicate content from other area docs -- link to them instead
