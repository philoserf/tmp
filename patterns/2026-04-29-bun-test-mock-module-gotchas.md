---
title: "Bun test mock.module gotchas"
type: pattern
project: "global"
tags: [tool/bun, lang/typescript, topic/testing, urgency/gotcha]
created: 2026-04-29
updated: 2026-04-29
status: active
---

Bun's `mock.module()` has subtle ordering and lifecycle constraints that cause silent test failures and misleading results.

## Order matters: mock before import

`mock.module(...)` must be called **before** `await import()` of the module under test. The dynamic import pattern is:

```ts
const mockCreate = mock();

mock.module("@some-package/sdk", () => {
  class Sdk {
    method = mockCreate;
  }
  return { default: Sdk };
});

// AFTER mock.module — top-level await imports the module with the mock in place.
const { thingUnderTest } = await import("./thingUnderTest");
```

If the import precedes the mock, the module captures the real implementation and the mock has no effect.

## State leaks across tests

Mock state persists across tests within the same file (and via shared module mocks, sometimes across files). Always `mockClear()` in `beforeEach` for any mock that records calls or returns values:

```ts
beforeEach(() => {
  mockCreate.mockClear();
});
```

Otherwise an earlier test's `mockResolvedValueOnce` chain may apply to a later test that didn't set its own.

## `null ?? default` is not the same as `value ?? default`

```ts
const file = "file" in opts ? opts.file : { extension: "md" };
```

Use the `"key" in opts` pattern when `null` is a valid test value distinct from "key absent". `null ?? default` returns the default and erases the test's intent to assert behavior on a null input.

## Project-specific extensions

When mocking framework SDKs, ensure every method exercised by the code path is present on the mock. Missing methods on a stub class fail with a non-obvious "method is not a function" rather than a clear "you forgot to mock X".

## Source

Originally captured on `philoserf/obsidian-metadator` (~2026-04-03) while writing tests for the Anthropic SDK adapter and Obsidian-Notice mocks. Migrated from per-project auto-memory to the agent memory vault on 2026-04-29.
