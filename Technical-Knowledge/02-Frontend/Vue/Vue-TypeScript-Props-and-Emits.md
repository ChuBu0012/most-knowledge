---
title: "Vue TypeScript Props and Emits"
type: concept
domain: vue with typescript
level: intermediate
tags: [vue, typescript, components]
status: researched
last_verified: 2026-11-20
sources:
  - https://vuejs.org/guide/typescript/composition-api.html
---

# Vue TypeScript Props and Emits

## Overview

Vue SFC สามารถอนุมาน props/emits ผ่าน `defineProps` และ `defineEmits` ทำให้ component contract อยู่ใกล้ template

## Mental model

ใน `<script setup lang="ts">` ใช้ type-based declarations สำหรับ props/emits; Vue compiler สร้าง runtime options ที่ทำได้จาก type. ใช้ `withDefaults` หรือ default value syntax ตาม Vue version. `defineModel` เป็น macro ที่ช่วย model binding แต่ควรเข้าใจ prop/event contract ที่อยู่เบื้องหลัง

## Example

```vue
<script setup lang="ts">
const props = defineProps<{ title: string; count?: number }>();
const emit = defineEmits<{ save: [id: string] }>();
</script>
```

Snippet is a focused pattern; include package imports, types, error handling, validation and runtime configuration from the installed release before production use.

## Common mistakes and trade-offs

type-based declaration ไม่สามารถสะท้อน type-level logic ทั้งหมดเป็น runtime validator ได้; event payload ต้องตรวจจาก data ภายนอก; อย่า mutate props โดยตรง

## Practical guidance

เปิด `vue-tsc`/language tools ใน CI, แยก type-only guarantees จาก runtime schema และเลือก `computed`/`emit` ตาม data ownership

## Related knowledge

[[Vue with TypeScript]] · [[Vue Reactivity and Computed State]] · [[TypeScript Type Narrowing]] · [[Zod Runtime Validation]]

## References

- [vuejs.org](https://vuejs.org/guide/typescript/composition-api.html)

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
