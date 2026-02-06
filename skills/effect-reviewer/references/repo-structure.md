# Constelia Monorepo Structure

## Directory Layout

```
packages/           Core libraries (reusable)
  ai/               AI model providers (Bedrock, Voyage, Ollama, mock)
  aws/              AWS SDK wrappers (S3, Bedrock Agent)
  config/           Typed config layers (Env, AWS, Postgres, LLM, etc.)
  contracts/        RPC/API type contracts
  db/               Drizzle ORM schemas, migrations, Effect SQL client
  error/            TaggedError definitions
  observability/    Tracing, logging, HTTP/RPC middleware
  vector-store/     pgvector queries and upserts

services/           Applications
  api/              Main backend (RPC, HTTP, WebSocket via @effect/platform)
  ingestion/        Data ingestion pipeline

scripts/            CLI tools and utilities
  rag-cli/          RAG query CLI

clients/
  browser/          React frontend (Vite + TanStack Router/Query)
```

## Dependency Hierarchy

```
Low-level:   config, error
Mid-level:   db, aws, ai, observability, contracts
High-level:  vector-store, services, browser
```

## tsconfig Hierarchy

```
tsconfig.base.json              Shared: paths aliases, strict, NodeNext
├── tsconfig.package.json       Packages: +declaration, +composite, +incremental
├── tsconfig.service.json       Services: +outDir, +composite
└── per-package/tsconfig.json   Extends one of the above
```

Every package/service/script MUST extend the base config to inherit `paths` aliases. Without this, `tsx` and `tsc` cannot resolve `@constelia/*` imports.

Per-package tsconfigs declare `references` for build ordering:

```json
{
  "extends": "../../tsconfig.package.json",
  "references": [{ "path": "../config" }, { "path": "../contracts" }]
}
```

## package.json Exports

Standard dual-condition pattern:

```json
{
  "exports": {
    ".": {
      "types": "./dist/index.d.ts",
      "development": "./src/index.ts",
      "default": "./dist/index.js"
    }
  }
}
```

- `development` condition: source `.ts` (active via `NODE_OPTIONS='--conditions=development'`)
- `default` condition: compiled `.js` from `dist/`

## Dependencies

- Internal packages: `"@constelia/db": "workspace:*"`
- Shared external versions: `"effect": "catalog:"` (defined in `pnpm-workspace.yaml`)

## Naming

| Pattern         | Usage                               |
| --------------- | ----------------------------------- |
| `*.schema.ts`   | Drizzle database schemas            |
| `*.test.ts`     | Test files                          |
| `*.executor.ts` | AI agent executors                  |
| `*.config.ts`   | Configuration files                 |
| `__tests__/`    | Test directories (alongside source) |

## Imports

- Cross-package: `import { Db } from '@constelia/db'`
- Local ESM: `import { foo } from './bar.js'` (always `.js` extension)
- Subpath exports: `import { makeTracingLive } from '@constelia/observability/tracing'`

## Barrel Exports

- Wildcard `export *` for flat modules (schemas)
- Named exports for feature modules with specific API surface (ai, contracts)

## Tooling

- **Biome**: Linting + formatting (tabs, single quotes)
- **Vitest**: Testing with `v8` coverage
- **Knip**: Dead code detection
- **pnpm**: Package manager with workspace + catalog support
