---
title: "React State and Batching"
type: concept
domain: react
level: intermediate
tags: [react, state]
status: researched
last_verified: 2026-11-20
sources:
  - https://react.dev/learn/queueing-a-series-of-state-updates
---

# React State and Batching

## Overview

state คือข้อมูลที่ React เก็บข้าม render; ทุก render อ่าน snapshot ของ state ชุดหนึ่ง

## กลไกและแนวคิดหลัก

เรียก setter เพื่อ queue การ update; React batch updates ที่เกิดใน event/async boundary ที่รองรับ แล้ว render ด้วยค่าถัดไป. เมื่ออัปเดตจากค่าเดิมซ้ำ ใช้ updater function เพื่อให้ต่อกันตาม queue. State ควร immutable เพราะ React ใช้ identity เปรียบเทียบและ object ที่ mutate อาจไม่ทำให้ UI เปลี่ยนตามคาด

## ตัวอย่าง

```tsx
const [count, setCount] = useState(0);
function addThree() {
  setCount(n => n + 1);
  setCount(n => n + 1);
  setCount(n => n + 1);
}
```

ตัวอย่างสาธิตแนวคิด ไม่ใช่ไฟล์แอปที่พร้อม deploy; ต้องเติม types/imports, error boundaries และการทดสอบตาม project setup

## จุดพลาดและข้อควรระวัง

อย่าเก็บค่าที่ derive จาก props/state ซ้ำเป็น state หากคำนวณระหว่าง render ได้; อย่า mutate array/object แล้วส่ง reference เดิมกลับ; อย่าคาดว่า setter เปลี่ยนค่าที่ handler ปัจจุบันอ่านอยู่

## แนวทางใช้งาน

ใช้ state สำหรับข้อมูลที่เปลี่ยนตาม interaction และมีผลต่อ UI; แยก server cache ไป [[TanStack-Query]] และ shared client state ไป [[Zustand]] เมื่อจำเป็น

## ความสัมพันธ์

[[React Rendering Model]] · [[React Component Identity and Keys]] · [[State-Management-Concepts]] · [[TanStack-Query]] · [[Zustand]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://react.dev/learn/queueing-a-series-of-state-updates)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
