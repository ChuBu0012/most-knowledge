---
title: "React Effect Synchronization"
type: concept
domain: react
level: intermediate
tags: [react, effects]
status: researched
last_verified: 2026-11-20
sources:
  - https://react.dev/learn/lifecycle-of-reactive-effects
---

# React Effect Synchronization

## Overview

Effect เชื่อม component กับระบบภายนอกที่ React ไม่ได้ควบคุม เช่น subscription, browser API หรือ third-party widget

## กลไกและแนวคิดหลัก

หลัง commit React เรียก Effect; ก่อนรัน effect ใหม่ที่ dependencies เปลี่ยน จะเรียก cleanup ของรอบก่อน. Dependencies สะท้อนค่าจาก render ที่ effect ใช้. หาก logic เพียงแปลง props/state เป็น UI ให้คำนวณใน render แทน useEffect

## ตัวอย่าง

```tsx
useEffect(() => {
  const connection = createConnection(roomId);
  connection.connect();
  return () => connection.disconnect();
}, [roomId]);
```

ตัวอย่างสาธิตแนวคิด ไม่ใช่ไฟล์แอปที่พร้อม deploy; ต้องเติม types/imports, error boundaries และการทดสอบตาม project setup

## จุดพลาดและข้อควรระวัง

Effect ที่ขาด dependency อ่านค่า stale; dependency ที่สร้าง object/function ใหม่ทุก render ทำให้ reconnect ซ้ำ; request race ต้องยกเลิกหรือ ignore ผลเก่าตอน cleanup

## แนวทางใช้งาน

ใช้ event handler สำหรับผลจาก user action, Effect สำหรับ sync lifecycle ภายนอก และ query library สำหรับ server data/cache

## ความสัมพันธ์

[[React Rendering Model]] · [[JavaScript Closures]] · [[TanStack-Query]] · [[Playwright]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://react.dev/learn/lifecycle-of-reactive-effects)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
