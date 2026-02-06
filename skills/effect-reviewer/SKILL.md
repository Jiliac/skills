---
name: effect-reviewer
description: Review code for idiomatic Effect-ts usage and Constelia monorepo conventions. Use when writing, reviewing, or modifying TypeScript code that uses the Effect library.
---

# Effect-ts & Constelia Code Reviewer

Review code for idiomatic Effect-ts patterns as used in this monorepo. Apply when writing new code, reviewing PRs, or refactoring existing Effect-based code.

## Core Rules

### Error Handling

- Use `Cause.RuntimeException` for wrapping external failures in `Effect.tryPromise` / `Effect.try` catch handlers. Never use `new Error()`.
- Use `Data.TaggedError` for internal/operational errors. Use `Schema.TaggedError` for domain errors needing structured fields.
- Use `Effect.fail()` for expected/recoverable errors. Use `Effect.die()` / `Effect.orDie` only for truly unrecoverable defects.
- Always provide a `catch` handler in `Effect.tryPromise({ try, catch })`. Bare `Effect.tryPromise(() => ...)` loses error context.

### Services & Layers

- Define services with `Context.Tag` (not `GenericTag`), with `layer` as a static property on the Tag class.
- Compose layers with `.pipe(Layer.provide(...))` for dependencies, `Layer.provideMerge` to accumulate.
- Apply `Layer.memoize` to prevent re-instantiation of shared services.
- Never chain multiple `Effect.provide()` calls in a pipe — merge layers and provide once. The Effect LSP warns about this.
- Export `Effect.serviceFunctionEffect` wrappers for common service operations.

### Generators

- Use `Effect.gen(function* () { ... })` for all effectful workflows.
- `yield*` is only for Effect values (services, configs, effects). Never `yield*` regular values.
- Use `Effect.forEach(..., { concurrency })` for batch operations with controlled parallelism.

### Config & Secrets

- Load config via `Config.string()`, `Config.number()`, `Config.literal()`, `Config.redacted()`.
- Extract redacted values with `Redacted.value(yield* SomeConfig)`.
- Use `Config.option` for optional config values, extract with `Option.getOrUndefined` / `Option.getOrElse`.

### Observability

- Wrap business operations with `Effect.withSpan('operationName', { attributes })`.
- Use `Effect.logInfo`, `Effect.logError`, `Effect.logDebug` — never `console.log`.

## Monorepo Conventions

- Read `references/repo-structure.md` for package layout, tsconfig hierarchy, and import patterns.
- All new packages/scripts must extend `tsconfig.base.json` (or `tsconfig.package.json` / `tsconfig.service.json`) to inherit path aliases.
- Use `workspace:*` for internal deps, `catalog:` for shared external deps.
- Local imports use `.js` extensions (ESM convention).
- File naming: `.schema.ts`, `.test.ts`, `.executor.ts`, `.config.ts`.
- Tests go in `__tests__/` directories alongside source.

## References

- `references/effect-patterns.md` — Complete Effect-ts patterns with code examples
- `references/repo-structure.md` — Monorepo layout, tsconfig, exports, and naming conventions
