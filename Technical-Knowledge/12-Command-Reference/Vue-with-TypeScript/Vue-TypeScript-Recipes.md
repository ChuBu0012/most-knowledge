---
title: Vue with TypeScript Recipes
type: reference
tags: [technical-knowledge, vue, typescript, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://vuejs.org/guide/typescript/overview.html
  - https://vuejs.org/guide/typescript/composition-api.html
---

# Vue with TypeScript Recipes

## Type props and defaults

```vue
<script setup lang="ts">
interface Props { userId: string; compact?: boolean }
const props = withDefaults(defineProps<Props>(), { compact: false })
</script>
```

Props are readonly inputs; do not mutate them. Use defaults for optional values with intentional semantics.

## Type emits

```ts
const emit = defineEmits<{
  save: [payload: { id: string; name: string }]
  cancel: []
}>()
```

Events express intent upward. Parent owns persistence/state transition.

## Type template refs

```ts
const input = ref<HTMLInputElement | null>(null)
onMounted(() => input.value?.focus())
```

DOM refs begin null and are only available after mount; optional chaining handles lifecycle.

## Type a composable

```ts
export function useSelection<T extends { id: string }>(items: Ref<T[]>) {
  const selectedId = ref<string | null>(null)
  const selected = computed(() => items.value.find(item => item.id === selectedId.value))
  return { selectedId, selected }
}
```

Use generics when the composable preserves a type relationship. Prefer inference; annotate public boundaries and exported reusable APIs.

## Type injection key

Use `InjectionKey<T>` with `provide`/`inject`; `inject(key)` may be undefined, so enforce provider presence or define a safe default.

## Check types

Run `vue-tsc --noEmit` in CI; Vite transpilation alone does not type-check TypeScript. Keep Vue, TypeScript and `vue-tsc` compatible.

## Read next

[[Vue API Recipes]] · [[TypeScript Recipes]] · [[Vue TypeScript Props and Emits]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
