# Master Architecture Template (00-ARCHITECTURE.md)

Use this as the skeleton for the master file. Adapt sections to the project.

````markdown
# [Project Name] -- Architecture Overview

> Last updated: [DATE]
> Source of truth for high-level architecture. Detailed docs in `01-` through `NN-` files.

---

## Quick Navigation

| #   | Area        | Doc                                  |
| --- | ----------- | ------------------------------------ |
| 01  | [Area Name] | [01-area-name.md](./01-area-name.md) |
| ... | ...         | ...                                  |

---

## What Is [Project Name]

[3 sentences: what it does, who uses it, key differentiator]

---

## Tech Stack

| Layer    | Technology | Notes |
| -------- | ---------- | ----- |
| Frontend | ...        | ...   |
| Backend  | ...        | ...   |
| Database | ...        | ...   |
| AI/ML    | ...        | ...   |
| Hosting  | ...        | ...   |

---

## Directory Map

\```
project/
├── src/
│ ├── [key-file] # [annotation]
│ ├── [directory]/ # [annotation]
│ ...
├── [backend-dir]/
│ ...
├── docs/ # This documentation suite
└── [config-files]
\```

**Scale:** ~N source files, N database tables, N API endpoints.

---

## [User Roles / Key Actors] (if applicable)

| Role | Description | Permissions |
| ---- | ----------- | ----------- |
| ...  | ...         | ...         |

---

## Core Data Flow (End to End)

\```

1. [STEP NAME]
   [Actor] does X → [System] does Y → Result Z

2. [STEP NAME]
   ...
   \```

---

## The N Architecture Areas

| #   | Area | Description     | Key Entry Points | Doc    |
| --- | ---- | --------------- | ---------------- | ------ |
| 01  | ...  | [2-3 sentences] | `file1`, `file2` | [link] |
| ... | ...  | ...             | ...              | ...    |

---

## Key Architectural Patterns

### [Pattern Name]

[2-3 sentences explaining the pattern and where it's used]

### [Pattern Name]

...

---

## Key Decisions & Legacy

- **[Decision Name]** ([date]): [What was decided and why]
- ...

---

## Cross-References

| Concept   | Primary Doc      | Section                   |
| --------- | ---------------- | ------------------------- |
| [concept] | [NN-doc-name.md] | [Exact ## Section Header] |
| ...       | ...              | ...                       |
````

## Guidelines

- Keep under 350 lines
- The directory map should annotate every important file/folder
- Data flow should show the complete user journey
- Cross-references must use exact `##` headings from target docs
- Add patterns only for things that are genuinely architectural (not obvious)
