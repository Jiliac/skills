# Effect-ts Patterns — Constelia

## Error Handling

### Cause.RuntimeException for external failures

```typescript
import { Cause, Effect } from "effect";

const result =
  yield *
  Effect.tryPromise({
    try: () => fetch(url),
    catch: (e) =>
      new Cause.RuntimeException(
        `Fetch failed: ${e instanceof Error ? e.message : String(e)}`,
      ),
  });
```

### TaggedError for domain errors

```typescript
// Data.TaggedError — internal/operational
export class DbError extends Data.TaggedError("DbError")<{
  reason: string;
}> {
  get message() {
    return `DB error: ${this.reason}`;
  }
}

// Schema.TaggedError — domain errors with structured fields
export class ChatNotFoundError extends S.TaggedError<ChatNotFoundError>()(
  "ChatNotFoundError",
  { id: S.String },
) {
  get message() {
    return `Chat not found: ${this.id}`;
  }
}
```

### Error mapping at RPC boundaries

```typescript
export const mapInternalErrors = <A, E, R>(
  effect: Effect.Effect<A, E, R>,
): Effect.Effect<A, RpcInternalError, R> =>
  Effect.mapError(effect, (e) => {
    const error = e as { _tag?: string; message?: string };
    return new RpcInternalError({ reason: error.message ?? String(e) });
  });
```

## Services & Layers

### Service definition

```typescript
export class AWSConfig extends Context.Tag('@app/AWSConfig')<
  AWSConfig,
  Schema.Schema.Type<typeof AWSConfigSchema>
>() {
  static readonly layer = Layer.effect(
    AWSConfig,
    Effect.gen(function* () {
      const config = yield* Config.all({ ... });
      return AWSConfig.of(validated);
    }),
  );
}
```

### Layer composition

```typescript
const envLayer = EnvConfig.layer;
const postgresLayer = PostgresConfig.layer.pipe(Layer.provide(envLayer));
const drizzleLayer = DrizzleConfig.layer.pipe(Layer.provide(postgresLayer));

export const AppConfigLive = Layer.unwrapEffect(
  envLayer.pipe(
    Layer.provideMerge(postgresLayer),
    Layer.provideMerge(drizzleLayer),
    Layer.memoize,
  ),
);
```

### Service function wrappers

```typescript
export const getLanguageModelEffect = (type: LanguageModelType) =>
  Effect.serviceFunctionEffect(AiModels, (ai) => ai.getLanguageModel)(type);
```

## Generators

### Standard pattern

```typescript
Effect.gen(function* () {
  const db = yield* Db; // yield* services
  const config = yield* EnvConfig; // yield* configs
  const result = yield* someEffect; // yield* effects
  const processed = result.map((x) => x); // NO yield* for regular values
  yield* Effect.logInfo("Done");
  return processed;
});
```

### Batch with concurrency

```typescript
yield *
  Effect.forEach(
    documents,
    (doc) =>
      Effect.gen(function* () {
        const done = yield* isProcessed(doc.id);
        if (done) return;
        yield* processDoc(doc);
      }),
    { concurrency: 1 },
  );
```

## Providing Dependencies

### Correct: single provide with merged layers

```typescript
effect.pipe(
  Effect.withSpan("operation"),
  Effect.provide(Layer.mergeAll(Db.layer, AiModelsLive, AppConfigLive)),
  Effect.scoped,
);
```

### Wrong: chained provides (Effect LSP warns)

```typescript
// DON'T — causes service lifecycle issues
effect.pipe(
  Effect.provide(Db.layer),
  Effect.provide(AiModelsLive),
  Effect.provide(AppConfigLive),
);
```

## Config

```typescript
const config =
  yield *
  Config.all({
    host: Config.string("POSTGRES_HOST"),
    port: Config.number("POSTGRES_PORT"),
    password: Config.redacted("POSTGRES_PASSWORD").pipe(Config.option),
  });

// Extract redacted
const key = Redacted.value(yield * VoyageApiKey);

// Optional
const value = Option.getOrUndefined(config.password);
```

## Streams

```typescript
// Create from queue
const stream = Stream.fromQueue(yield * Queue.unbounded<string>());

// Unwrap Effect that returns Stream
Stream.unwrap(
  Effect.gen(function* () {
    const data = yield* loadData();
    return Stream.fromIterable(data).pipe(
      Stream.mapError((e) => new CustomError({ reason: String(e) })),
    );
  }),
);

// Error handling
stream.pipe(
  Stream.mapError((e) => new StreamError({ original: String(e) })),
  Stream.catchAll((error) =>
    Stream.fromEffect(
      Effect.logError("error", error).pipe(Effect.as(fallbackValue)),
    ),
  ),
);
```

## Testing

```typescript
// Provide mock layers
const result = await Effect.runPromise(
  myEffect.pipe(Effect.provide(Layer.succeed(Db, mockDb))),
);

// Test failures
const exit = await Effect.runPromiseExit(
  myEffect.pipe(Effect.provide(Layer.succeed(Db, failingDb))),
);
expect(exit._tag).toBe("Failure");
```

## Observability

```typescript
yield *
  Effect.gen(function* () {
    yield* Effect.annotateCurrentSpan({ userId: user.id });
    // work
  }).pipe(Effect.withSpan("handleChat", { attributes: { chatId } }));
```
