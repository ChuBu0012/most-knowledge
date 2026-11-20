---
title: Zustand Recipes
type: reference
tags: [technical-knowledge, zustand, react, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://zustand.docs.pmnd.rs/getting-started/introduction
---

# Zustand Recipes

## Create a store

```ts
import { create } from 'zustand'
type Cart = { count: number; add: () => void; clear: () => void }
export const useCart = create<Cart>()((set) => ({
  count: 0,
  add: () => set(state => ({ count: state.count + 1 })),
  clear: () => set({ count: 0 }),
}))
```

Store actions live beside state. `set` shallow-merges top-level state; replace nested objects explicitly instead of mutating them.

## Subscribe to a slice

```tsx
const count = useCart(state => state.count)
```

Selectors limit rerenders to selected values. If returning a new object/array each call, use `useShallow` or a stable selector; otherwise equality may trigger avoidable renders.

## Async action

```ts
load: async (id) => {
  set({ loading: true, error: null })
  try { const item = await api.getItem(id); set({ item }) }
  catch (error) { set({ error: toMessage(error) }) }
  finally { set({ loading: false }) }
```

Model loading/error explicitly and prevent stale requests overwriting newer selections; use AbortController or request identity where needed.

## Persist selected state

Wrap with `persist` middleware and provide a stable storage key. Persist only durable client preferences/cart draft; avoid tokens or sensitive personal data in localStorage. Handle schema/version migration and hydration timing.

## Debug and test

Use `devtools` middleware in development. For tests, create a fresh store per test or reset state in teardown; avoid test-order dependence from module singleton state.

## Read next

[[Zustand Store Selectors and Persistence]] · [[React Recipes]] · [[TanStack Query Cache Lifecycle]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
