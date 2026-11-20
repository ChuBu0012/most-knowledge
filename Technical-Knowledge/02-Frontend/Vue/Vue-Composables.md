---
title: "Vue Composables"
type: concept
domain: vue
level: intermediate
tags: [vue, composables]
status: researched
last_verified: 2026-11-20
sources:
  - https://vuejs.org/guide/reusability/composables.html
---

# Vue Composables

## Overview

composable คือ function ที่ใช้ Composition API เพื่อรวม stateful behavior และให้ component นำไปประกอบใช้ซ้ำ

## กลไกและแนวคิดหลัก

Composable สามารถสร้าง reactive state ต่อ instance, register lifecycle hooks และคืน refs/actions. การเรียกใน setup/composable ที่ถูกต้องทำให้ Vue ผูก effect กับ component lifecycle; module-level ref จะกลายเป็น shared singleton ที่ทุกผู้ใช้เห็นร่วมกัน

## ตัวอย่าง

```vue
function useCounter() {
  const count = ref(0);
  const increment = () => count.value++;
  return { count, increment };
}
```

ตัวอย่างสาธิตแนวคิด ไม่ใช่ไฟล์แอปที่พร้อม deploy; ต้องเติม types/imports, error boundaries และการทดสอบตาม project setup

## จุดพลาดและข้อควรระวัง

อย่าซ่อน side effects ระดับ module โดยไม่ได้ตั้งใจ; SSR singleton state อาจรั่วข้าม request/user; คืน object ที่รักษา ref semantics หรือใช้ `toRefs` เมื่อต้อง destructure reactive object

## แนวทางใช้งาน

ตั้งชื่อ `use...`, แยก pure transformation ออกจาก stateful composable และออกแบบ cleanup สำหรับ timer/subscription/network

## ความสัมพันธ์

[[Vue Reactivity and Computed State]] · [[Nuxt]] · [[Pinia]] · [[VeeValidate]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://vuejs.org/guide/reusability/composables.html)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง
