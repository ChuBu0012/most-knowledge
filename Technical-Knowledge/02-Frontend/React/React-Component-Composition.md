---
title: "React Component Composition"
type: concept
domain: react
level: intermediate
tags: [react, components, architecture]
status: researched
last_verified: 2026-11-20
sources:
  - https://react.dev/learn/passing-props-to-a-component
---

# React Component Composition

## Overview

composition ใช้ประกอบ component เล็กเป็น tree และส่งความรับผิดชอบ/เนื้อหาผ่าน props แทนการสร้าง component ที่รู้จักทั้งแอป

## กลไกและแนวคิดหลัก

ใช้ `children` หรือ named slots เพื่อให้ parent ควบคุม layout ขณะที่ child เป็นผู้ส่ง content; ยก state ขึ้นเฉพาะจุดที่หลายส่วนต้องใช้ร่วม. Context เหมาะกับข้อมูลที่หลายชั้นต้องอ่านและเปลี่ยนไม่ถี่ ไม่ใช่ทางแทน prop ทุกกรณี

## ตัวอย่าง

```tsx
function Panel({ title, children }: PropsWithChildren<{title: string}>) {
  return <section><h2>{title}</h2>{children}</section>;
}
```

ตัวอย่างสาธิตแนวคิด ไม่ใช่ไฟล์แอปที่พร้อม deploy; ต้องเติม types/imports, error boundaries และการทดสอบตาม project setup

## จุดพลาดและข้อควรระวัง

component ที่รับ boolean props จำนวนมากจนมี state combination เยอะมักมีหน้าที่กว้างเกินไป; อย่าใส่ state กลางสูงสุดของแอปถ้าใช้แค่ subtree เดียว

## แนวทางใช้งาน

ออกแบบ public props ให้สื่อ intent, แยก primitive behavior ออกจาก domain data fetching และระบุ owner ของ state อย่างชัดเจน

## ความสัมพันธ์

[[React State and Batching]] · [[React Rendering Model]] · [[Zustand]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://react.dev/learn/passing-props-to-a-component)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง
