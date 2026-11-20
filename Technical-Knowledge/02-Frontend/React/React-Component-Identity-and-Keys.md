---
title: "React Component Identity and Keys"
type: concept
domain: react
level: intermediate
tags: [react, reconciliation]
status: researched
last_verified: 2026-11-20
sources:
  - https://react.dev/learn/preserving-and-resetting-state
---

# React Component Identity and Keys

## Overview

ตำแหน่ง component และ `key` กำหนดว่า React มอง UI element เป็น instance เดิมหรือ instance ใหม่ จึงมีผลต่อการคง/reset state

## กลไกและแนวคิดหลัก

React จับคู่ child ภายในตำแหน่ง parent โดยชนิด element และ key. ใน list ให้ใช้ stable key ที่มาจาก identity ของข้อมูล ไม่ใช่ index หากรายการ reorder/insert/delete เพราะ index ทำให้ state ของ input ย้ายไปติด record ผิดตัว. เปลี่ยน key อย่างตั้งใจเพื่อ reset subtree ได้

## ตัวอย่าง

```tsx
{todos.map(todo => (
  <TodoRow key={todo.id} todo={todo} />
))}
```

ตัวอย่างสาธิตแนวคิด ไม่ใช่ไฟล์แอปที่พร้อม deploy; ต้องเติม types/imports, error boundaries และการทดสอบตาม project setup

## จุดพลาดและข้อควรระวัง

ใช้ random key ทุก render จะทำให้ React unmount/mount ใหม่ สูญ state และ DOM focus; index key ใช้ได้เฉพาะ list คงที่ที่ไม่ reorder/remove/insert

## แนวทางใช้งาน

เก็บ state ของแต่ละรายการใน component ที่มี stable identity; ทดสอบ reorder กับ input state เพื่อพบ bug ที่มองไม่เห็นจาก static list

## ความสัมพันธ์

[[React Rendering Model]] · [[React State and Batching]] · [[React Component Composition]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://react.dev/learn/preserving-and-resetting-state)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง
