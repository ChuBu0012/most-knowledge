---
title: "Vue Reactivity and Computed State"
type: concept
domain: vue
level: intermediate
tags: [vue, reactivity]
status: researched
last_verified: 2026-11-20
sources:
  - https://vuejs.org/guide/essentials/reactivity-fundamentals.html
---

# Vue Reactivity and Computed State

## Overview

Vue reactivity ติดตามการอ่าน reactive state ระหว่างการประมวลผล แล้ว trigger effects เมื่อ property ที่อ่านถูกเปลี่ยน

## กลไกและแนวคิดหลัก

`ref` เก็บค่าใน `.value` ฝั่ง JavaScript; template unwrap ให้อัตโนมัติ. `computed` สร้างค่า derive แบบ lazy และ cache ตาม dependencies. `watch` ใช้ side effect เมื่อค่าที่ระบุเปลี่ยน และควรใช้เมื่อมีงานภายนอก ไม่ใช่เพื่อคำนวณค่า display

## ตัวอย่าง

```vue
const first = ref('Ada');
const last = ref('Lovelace');
const fullName = computed(() => `${first.value} ${last.value}`);
```

ตัวอย่างสาธิตแนวคิด ไม่ใช่ไฟล์แอปที่พร้อม deploy; ต้องเติม types/imports, error boundaries และการทดสอบตาม project setup

## จุดพลาดและข้อควรระวัง

destructure reactive object ตรง ๆ อาจทำให้สูญเสีย reactive connection; deep watch อาจแพงและให้ old/new object reference เดียวกันเมื่อ nested mutation; เลือก shallow/ref/reactive ให้ตรง data shape

## แนวทางใช้งาน

ชอบ computed สำหรับ derived state, ใช้ watch ระบุ source ให้แคบ และหยุด watcher/cleanup resource ตาม lifecycle

## ความสัมพันธ์

[[Vue]] · [[Vue with TypeScript]] · [[Pinia]] · [[VeeValidate]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://vuejs.org/guide/essentials/reactivity-fundamentals.html)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
