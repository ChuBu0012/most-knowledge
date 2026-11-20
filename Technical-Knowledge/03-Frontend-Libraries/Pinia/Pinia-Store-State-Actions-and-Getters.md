---
title: "Pinia Store State Actions and Getters"
type: concept
domain: pinia
level: intermediate
tags: [pinia, vue, state]
status: researched
last_verified: 2026-11-20
sources:
  - https://pinia.vuejs.org/core-concepts/
---

# Pinia Store State Actions and Getters

## Overview

Pinia store รวม state, actions และ getters ภายใต้ id ที่เรียกซ้ำจาก component/composable ได้; Vue reactivity ทำให้ UI ติดตามการเปลี่ยน state

## Mental model

`defineStore` สร้าง store; Setup Store ใช้ refs เป็น state, computed เป็น getters และ functions เป็น actions. `storeToRefs` ช่วย destructure state/getters โดยรักษา reactivity; actions รับ async work ได้. SSR ต้องแยก Pinia instance ต่อ app/request และใช้ Nuxt integration ที่เหมาะสม

## Example

```vue
export const useCounter = defineStore('counter', () => {
  const count = ref(0);
  const double = computed(() => count.value * 2);
  function increment() { count.value++; }
  return { count, double, increment };
});
```

Snippet is a focused pattern; include package imports, types, error handling, validation and runtime configuration from the installed release before production use.

## Common mistakes and trade-offs

destructure store field ตรง ๆ อาจทำให้ reactivity หาย; setup store ที่คืน state ไม่ครบกระทบ devtools/SSR; module singleton ระดับ server อาจทำ state leak ข้าม request

## Practical guidance

ตั้ง store ต่อ domain, เก็บ server state ใน query/cache layer ถ้ามี, ใช้ actions กับ business transition ที่ซ้ำ และ persist เฉพาะ state ที่ควรอยู่ข้าม reload

## Related knowledge

[[Pinia]] · [[Vue Reactivity and Computed State]] · [[Vue Composables]] · [[State-Management-Concepts]]

## References

- [pinia.vuejs.org](https://pinia.vuejs.org/core-concepts/)
