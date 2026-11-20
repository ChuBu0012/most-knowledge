---
title: Pinia Recipes
type: reference
tags: [technical-knowledge, pinia, vue, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://pinia.vuejs.org/core-concepts/
---

# Pinia Recipes

## Create and register Pinia

```ts
// main.ts
const app = createApp(App)
app.use(createPinia())
app.mount('#app')
```

## Define a setup store

```ts
export const useCounterStore = defineStore('counter', () => {
  const count = ref(0)
  const doubled = computed(() => count.value * 2)
  function increment() { count.value++ }
  return { count, doubled, increment }
})
```

Use stable unique store IDs. State is per Pinia instance; avoid module-level user state shared across SSR requests.

## Read store values in component

```ts
const store = useCounterStore()
const { count, doubled } = storeToRefs(store)
const { increment } = store
```

Destructuring reactive state directly loses reactivity; `storeToRefs` preserves state/getters while actions can be destructured normally.

## Update state

Use `store.count++` for a direct mutation; `$patch({ count: 10 })` for grouped fields; `$patch(state => { ... })` for complex in-place updates. Keep business rules in actions when multiple consumers need the same behavior.

## Async action

```ts
async function loadUser(id: string) {
  this.loading = true
  try { this.user = await api.getUser(id) }
  finally { this.loading = false }
}
```

Track errors as well as loading; cancellation/stale response handling is necessary when selected ID can change rapidly.

## Subscribe and persist

`store.$subscribe((mutation, state) => ...)` observes state changes; unsubscribe on component lifecycle if subscription is local. Persistence plugins need an allowlist and versioned migration; do not persist secrets by default.

## Read next

[[Pinia Store State Actions and Getters]] · [[Vue API Recipes]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
