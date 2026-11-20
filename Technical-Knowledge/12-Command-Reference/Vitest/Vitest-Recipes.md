---
title: Vitest Recipes
type: reference
tags: [technical-knowledge, vitest, testing, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://vitest.dev/guide/
  - https://vitest.dev/api/
---

# Vitest Recipes

## Install and run

```sh
npm install -D vitest
npx vitest run
npx vitest --watch
```

Use watch mode locally; CI should use deterministic `run` and report coverage explicitly.

## Write a unit test

```ts
import { describe, expect, it } from 'vitest'
import { total } from './cart'

describe('total', () => {
  it('sums item prices and quantities', () => {
    expect(total([{ price: 12, quantity: 2 }])).toBe(24)
  })
})
```

Test observable behavior and edge cases; avoid mirroring implementation line by line.

## Mock module or function

Use `vi.mock()` for module boundary and `vi.fn()`/`vi.spyOn()` for specific calls. Reset/restore mocks between tests; do not let call history leak across cases. Prefer dependency injection for core business logic.

## Test async rejection

```ts
await expect(loadUser('missing')).rejects.toThrow('not found')
```

Await promise assertions so test runner observes completion. Use fake timers only when testing timer behavior; restore real timers after each test.

## Test React component

Use Testing Library queries by role/label/text and `userEvent` for realistic interactions. Query visible semantics, not implementation-specific class names. Keep browser/E2E testing for real navigation/network integration.

## Configure setup and coverage

Set `test` include/environment/setupFiles in Vite config. Coverage thresholds should reflect meaningful critical paths and exclude generated files; coverage percentage alone is not correctness.

## Read next

[[Unit Integration and End-to-End Tests]] · [[Playwright Recipes]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
