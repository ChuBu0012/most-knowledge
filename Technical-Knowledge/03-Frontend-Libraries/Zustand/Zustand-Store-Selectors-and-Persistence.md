---
title: "Zustand Store Selectors and Persistence"
type: concept
domain: zustand
level: intermediate
tags: [zustand, state, react]
status: researched
last_verified: 2026-11-20
sources:
  - https://zustand.docs.pmnd.rs/integrations/persisting-store-data
---

# Zustand Store Selectors and Persistence

## Overview

Zustand store เก็บ client state นอก component; component subscribe เฉพาะ selected slice เพื่อหลีกเลี่ยง render ที่ไม่เกี่ยวข้อง

## Mental model

`create` คืน hook ที่อ่าน/subscribe store; `set` merge partial state โดย default และ `get` อ่าน snapshot ปัจจุบันภายใน action. Selectors ควรคืน primitive/reference ที่ stable หรือใช้ shallow comparison. `persist` serializes selected fields to storage; async storage ทำให้ hydration asynchronous (Zustand 5.1 `rehydrate()` คืน Promise)

## Example

```tsx
const useCart = create<CartState>()((set) => ({
  items: [],
  add: item => set(state => ({ items: [...state.items, item] })),
}));
const count = useCart(state => state.items.length);
```

Snippet is a focused pattern; include package imports, types, error handling, validation and runtime configuration from the installed release before production use.

## Common mistakes and trade-offs

persist token/secret ใน localStorage เพิ่ม XSS impact; selector ที่คืน object ใหม่ทุกครั้งทำให้ render บ่อย; SSR store singleton อาจรั่ว state ข้าม user; async hydration อาจทำ UI flash

## Practical guidance

เก็บเฉพาะ client-owned state, whitelist partialize, version/migrate persisted data, create store per request for SSR where needed, and await hydration where correctness depends on restored state

## Related knowledge

[[Zustand]] · [[State-Management-Concepts]] · [[React State and Batching]] · [[Cookie and Session Security]]

## References

- [zustand.docs.pmnd.rs](https://zustand.docs.pmnd.rs/integrations/persisting-store-data)
