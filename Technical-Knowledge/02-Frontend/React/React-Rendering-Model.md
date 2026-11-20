---
title: "React Rendering Model"
type: concept
domain: react
level: intermediate
tags: [react, rendering]
status: researched
last_verified: 2026-11-20
sources:
  - https://react.dev/learn/render-and-commit
---

# React Rendering Model

## Overview

React render คือการเรียก component เพื่อคำนวณคำอธิบาย UI จาก props, state และ context ในรอบนั้น ไม่ใช่คำสั่งวาด DOM โดยตรง

## กลไกและแนวคิดหลัก

เมื่อ state/props/context เปลี่ยน React เรียก component ที่เกี่ยวข้องเพื่อสร้าง element tree ใหม่ จากนั้น reconcile tree แล้ว commit เฉพาะ DOM changes ที่จำเป็น Render ต้องบริสุทธิ์: ห้ามทำ network request, mutate global data หรือแก้ DOM ระหว่าง render. React อาจเรียก render ซ้ำหรือทิ้งผล render ที่ยังไม่ commit ได้

## ตัวอย่าง

```tsx
function Greeting({ name }: { name: string }) {
  return <h1>Hello, {name}</h1>;
}
```

ตัวอย่างสาธิตแนวคิด ไม่ใช่ไฟล์แอปที่พร้อม deploy; ต้องเติม types/imports, error boundaries และการทดสอบตาม project setup

## จุดพลาดและข้อควรระวัง

state setter ขอให้ React render รอบใหม่ ไม่ได้เปลี่ยนค่าตัวแปรใน render ปัจจุบันทันที; event handler ที่ closure มาจาก render เดิมจึงเห็น snapshot เดิม. Strict Mode ใน development อาจเรียกบาง logic ซ้ำเพื่อค้น side effect ที่ผิดตำแหน่ง

## แนวทางใช้งาน

แยกการคำนวณ UI ออกจาก side effect, เก็บ state ให้ใกล้ component ที่ใช้ และ profile ก่อน optimize ด้วย memoization

## ความสัมพันธ์

[[React State and Batching]] · [[React Component Identity and Keys]] · [[React Effect Synchronization]] · [[React Server and Client Components]] · [[React with TypeScript]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://react.dev/learn/render-and-commit)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
