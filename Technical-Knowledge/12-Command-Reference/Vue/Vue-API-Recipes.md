---
title: Vue API Recipes
type: reference
domain: vue
tags: [technical-knowledge, vue, api-reference, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://vuejs.org/api/reactivity-core.html
  - https://vuejs.org/guide/essentials/reactivity-fundamentals.html
  - https://vuejs.org/guide/essentials/watchers.html
  - https://vuejs.org/guide/components/props.html
  - https://vuejs.org/guide/components/events.html
  - https://vuejs.org/guide/reusability/composables.html
---

# Vue API Recipes

คู่มือค้นจากสิ่งที่ต้องการทำ ใช้ Vue 3 Composition API กับ `<script setup>` เป็นหลัก; ถ้าโปรเจกต์ใช้ Options API ให้เทียบแนวคิดที่ [[Vue|overview]]. ตัวอย่างสมมติว่าไฟล์เป็น `.vue` และลงทะเบียน component ตามปกติ

## เริ่ม component

```vue
<script setup lang="ts">
import { ref } from 'vue'

const count = ref(0)
function increment() {
  count.value++
}
</script>

<template>
  <button @click="increment">นับ {{ count }}</button>
</template>
```

ใน JavaScript/TypeScript ต้องอ่าน/เขียน `.value`; ใน template ref ชั้นบนสุดจะ unwrap ให้อัตโนมัติ. ใช้ `ref` เป็นค่าเริ่มต้นสำหรับ state ที่เปลี่ยนได้ รวมถึง primitive และ object ที่ต้องแทนที่ทั้งก้อน.

## สร้าง state: `ref` กับ `reactive`

```ts
import { reactive, ref } from 'vue'

const page = ref(1)
page.value++

const filters = reactive({ query: '', activeOnly: false })
filters.query = 'vue'
```

- `ref(initial)` คืน Ref object; เหมาะกับ primitive, ค่า async และกรณีต้องเปลี่ยนทั้ง object (`user.value = nextUser`).
- `reactive(object)` คืน Proxy; อ่าน/เขียน property โดยตรง เหมาะกับ object ที่คง identity.
- หลีกเลี่ยง destructure property จาก reactive object ตรง ๆ เพราะ local binding จะไม่รักษาการเชื่อม reactivity; ใช้ `toRef(filters, 'query')` หรือ `toRefs(filters)`.
- ใช้ `shallowRef` เมื่อเก็บ instance/object ใหญ่ที่ไม่ต้อง proxy ลึก แล้วเรียก `triggerRef` เฉพาะเมื่อจำเป็น.

## คำนวณค่าจาก state: `computed`

```ts
import { computed, ref } from 'vue'

const price = ref(120)
const quantity = ref(2)
const total = computed(() => price.value * quantity.value)
```

`computed` cache ผลตาม reactive dependencies และคำนวณใหม่เมื่อ dependency เปลี่ยน. ใช้มันกับค่าที่ derive ได้ เช่น total, filtered list, validation summary; อย่าใช้ `watch` เพื่อคัดลอกค่าที่ `computed` คำนวณได้อยู่แล้ว.

Writable computed ใช้เมื่อมี mapping ไป/กลับที่ชัดเจน:

```ts
const first = ref('Ada')
const last = ref('Lovelace')
const fullName = computed({
  get: () => `${first.value} ${last.value}`,
  set: (value: string) => {
    ;[first.value, last.value] = value.split(' ', 2)
  },
})
```

## ทำ side effect เมื่อค่าถูกเปลี่ยน: `watch`

```ts
import { ref, watch } from 'vue'

const userId = ref('u-1')
const user = ref<User | null>(null)
const error = ref<unknown>(null)

watch(userId, async (id, _oldId, onCleanup) => {
  const controller = new AbortController()
  onCleanup(() => controller.abort())
  error.value = null
  try {
    const response = await fetch(`/api/users/${id}`, { signal: controller.signal })
    if (!response.ok) throw new Error(`HTTP ${response.status}`)
    user.value = await response.json() as User
  } catch (cause) {
    if (!controller.signal.aborted) error.value = cause
  }
}, { immediate: true })
```

`watch(source, callback)` ติดตาม source ที่ระบุและให้ค่าเก่า/ใหม่; เหมาะกับ network, storage, analytics หรือเชื่อมระบบภายนอก. ใช้ cleanup ยกเลิกงานเก่าก่อนผลตอบกลับจะเขียนทับข้อมูลใหม่. ค่าเริ่มต้น callback ทำงานหลัง DOM update; `flush: 'post'` ใช้เมื่ออ่าน DOM หลัง render และ `flush: 'sync'` ใช้เฉพาะเมื่อจำเป็นจริงเพราะอาจเรียกถี่.

### เมื่อใดใช้ `watchEffect`

```ts
import { watchEffect } from 'vue'

watchEffect((onCleanup) => {
  const controller = new AbortController()
  onCleanup(() => controller.abort())
  void fetch(`/api/search?q=${encodeURIComponent(filters.query)}`, {
    signal: controller.signal,
  })
})
```

`watchEffect` เก็บ dependency ที่ถูกอ่านระหว่าง synchronous execution โดยอัตโนมัติ; ใช้เมื่อ dependencies หลายตัวและอ่านออกชัด. ถ้าต้องควบคุม trigger, old value หรืออ่าน dependency หลัง `await`, เลือก `watch` แทน.

## ยก state จาก component: `toRef` / `toRefs`

```ts
import { reactive, toRefs } from 'vue'
const state = reactive({ page: 1, query: '' })
const { page, query } = toRefs(state) // ทั้งคู่ยังเชื่อมกับ state
```

ใช้ใน composable เมื่อคืนหลาย property แล้ว consumer อยาก destructure. `toRef(props, 'modelValue')` สร้าง ref ที่เชื่อม property เดียว แต่ props ยังอ่านอย่างเดียว; ส่ง event กลับเพื่อเปลี่ยนค่า.

## รับข้อมูลจาก parent: `defineProps`

```vue
<script setup lang="ts">
const props = defineProps<{ userId: string; compact?: boolean }>()
</script>
```

Runtime defaults/validators:

```ts
const props = withDefaults(defineProps<{ title: string; count?: number }>(), {
  count: 0,
})
```

Props เป็น input read-only. อย่าแก้ `props.count`; derive ด้วย `computed`, หรือส่ง intent ขึ้นด้วย event.

## ส่ง intent ขึ้น: `defineEmits`

```vue
<script setup lang="ts">
const emit = defineEmits<{
  save: [value: { title: string }]
  cancel: []
}>()
function submit() {
  emit('save', { title: 'Draft' })
}
</script>
```

Parent ใช้ `<Editor @save="saveDraft" />`. Event คือสัญญาการสื่อสาร; component ลูกควรแจ้งว่าผู้ใช้ทำอะไร ส่วน parent เป็นเจ้าของการบันทึก/เปลี่ยน route.

## ทำ two-way binding ด้วย `v-model`

Component Vue 3.4+:

```vue
<script setup lang="ts">
const model = defineModel<string>({ required: true })
</script>
<template><input v-model="model"></template>
```

Parent: `<NameInput v-model="name" />`. ใช้ `defineModel('open')` กับ named model (`v-model:open`). ถ้าใช้ API แบบเก่ากว่า 3.4 ให้ประกาศ prop `modelValue` และ emit `update:modelValue`. หลีกเลี่ยง default ที่ทำให้ค่าฝั่ง child กับ parent ไม่ตรงกัน.

## อ่าน DOM หลัง mount: lifecycle และ template ref

```vue
<script setup lang="ts">
import { onMounted, onUnmounted, ref } from 'vue'
const input = ref<HTMLInputElement | null>(null)
let timer: ReturnType<typeof setInterval> | undefined
onMounted(() => {
  input.value?.focus()
  timer = setInterval(refresh, 5_000)
})
onUnmounted(() => clearInterval(timer))
</script>
<template><input ref="input"></template>
```

เข้าถึง DOM เฉพาะหลัง mount; cleanup timer, listener และ subscription ตอน unmount. SSR ไม่มี `onMounted` บน server. ถ้า DOM ต้องรอ state-driven render ให้ `await nextTick()` ก่อนอ่าน.

## ใช้ slot ส่งเนื้อหา/ข้อมูลกลับไปยัง caller

```vue
<!-- DataList.vue -->
<template>
  <ul><li v-for="item in items" :key="item.id"><slot :item="item" /></li></ul>
</template>
```

Parent: `<DataList v-slot="{ item }">{{ item.name }}</DataList>`. ใช้ slot เมื่อ caller ควรควบคุม markup; ใช้ props/events เมื่อ component ต้องมี contract ข้อมูล/intent ชัดเจน.

## แชร์ logic: composable `use…`

```ts
// useCounter.ts
import { computed, ref } from 'vue'
export function useCounter(initial = 0) {
  const count = ref(initial)
  const doubled = computed(() => count.value * 2)
  function increment() { count.value++ }
  return { count, doubled, increment }
}
```

Composable รวม stateful logic โดยไม่รวม UI. คืน ref แยกให้ destructure ได้; ระวัง state ที่สร้างนอก function จะกลายเป็น shared singleton ระหว่างทุก consumer/SSR request.

## แชร์ dependency ใน subtree: `provide` / `inject`

```ts
import { inject, provide, type InjectionKey, ref } from 'vue'
const themeKey: InjectionKey<Ref<'light' | 'dark'>> = Symbol('theme')
provide(themeKey, ref('light'))
const theme = inject(themeKey)
if (!theme) throw new Error('Theme provider is missing')
```

เหมาะกับ dependency เชิง subtree เช่น theme หรือ form context; อย่าใช้แทน global store โดยไม่จำเป็น. ใช้ Symbol typed key และจัดการกรณีไม่มี provider.

## สั่ง directive ใน template ที่ใช้บ่อย

```vue
<template>
  <p v-if="ready">conditional</p>
  <p v-show="visible">toggle display</p>
  <li v-for="row in rows" :key="row.id">{{ row.name }}</li>
  <button :disabled="saving" @click="save">{{ saving ? 'Saving…' : 'Save' }}</button>
  <input v-model.trim="name" />
</template>
```

- `v-if`: สร้าง/ถอด subtree; ใช้เมื่อเงื่อนไขไม่เปลี่ยนถี่.
- `v-show`: คง DOM แล้วสลับ CSS display; ใช้เมื่อ toggle บ่อย.
- `v-for`: ใส่ `:key` ที่ stable และไม่ซ้ำ; อย่าใช้ array index เมื่อรายการ reorder ได้.
- `v-on`/`@`: event; `.prevent`, `.stop` ใช้กับ native event เฉพาะเมื่อพฤติกรรมต้องการ.
- `v-model`: binding form input; modifier เช่น `.trim`, `.number` แปลง input ตามต้องการ.

## เลือก API ให้ตรงงาน

| อยากทำอะไร | ใช้ | เหตุผล |
|---|---|---|
| เก็บค่าที่แก้ได้ | `ref` | รองรับค่าหลายชนิดและแทนค่าทั้งก้อนได้ |
| เก็บ object ที่แก้ property เดิม | `reactive` | อ่าน/เขียน field ตรง ๆ |
| derive ค่า | `computed` | cache ตาม dependencies; ไม่มี side effect |
| เรียกงานเมื่อ source เปลี่ยน | `watch` | ควบคุม source/old-new/cleanup ได้ |
| effect จาก dependencies ที่อ่าน | `watchEffect` | เก็บ dependency อัตโนมัติ |
| แชร์ logic | composable | reuse behavior และ stateful logic |
| ส่งข้อมูลลง | props | parent เป็นเจ้าของ input |
| ส่งเหตุการณ์ขึ้น | emits | child แจ้ง intent ไม่แก้ parent state โดยตรง |

## จุดผิดพลาดที่พบบ่อย

1. ลืม `.value` ใน script แต่ template ไม่ต้องใส่กับ top-level refs.
2. destructure จาก `reactive` แล้วเสีย reactivity; ใช้ `toRefs`.
3. ใช้ `watch` คัดลอก state ทั้งที่ `computed` ทำได้.
4. fetch ใน watcher โดยไม่ abort งานเก่า; request เก่าอาจทับ response ใหม่.
5. แก้ props โดยตรง; ส่ง event หรือใช้ `defineModel`.
6. ลืม `:key`/ใช้ index เป็น key กับ list ที่ reorder.
7. สร้าง mutable singleton ใน module ระดับบนสุดของ SSR แล้วข้อมูลผู้ใช้รั่วข้าม request.

## ต่อไปอ่าน

- [[Vue Reactivity and Computed State]] — proxy/ref และ dependency tracking
- [[Vue Composables]] — ออกแบบ composable ที่ใช้ซ้ำ
- [[Vue with TypeScript]] — props, emits และ type inference
- [Vue Reactivity API](https://vuejs.org/api/reactivity-core.html)
- [Vue Watchers](https://vuejs.org/guide/essentials/watchers.html)

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
