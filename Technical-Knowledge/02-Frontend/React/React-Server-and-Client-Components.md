---
title: "React Server and Client Components"
type: concept
domain: react
level: intermediate
tags: [react, server-components, security]
status: researched
last_verified: 2026-11-20
sources:
  - https://react.dev/reference/rsc/server-components
---

# React Server and Client Components

## Overview

Server Components และ Client Components แบ่งงาน render ระหว่าง server กับ browser; boundary มีผลต่อ code ที่ส่งไป client และ capabilities ที่ใช้ได้

## กลไกและแนวคิดหลัก

Server Components ทำงานบน server/build environment และใช้ server-only capabilities ได้; Client Components ต้องระบุ directive use client ที่ boundary และ bundle dependency ของ subtree ไป browser. Props ที่ข้าม boundary ต้อง serialize ได้ตาม framework. Server Component ไม่ได้แทน authorization: ทุก operation ที่เปลี่ยนข้อมูลต้องตรวจสิทธิ์ฝั่ง server

## ตัวอย่าง

```tsx
// Client boundary
'use client';
import { useState } from 'react';
export function Counter() {
  const [n, setN] = useState(0);
  return <button onClick={() => setN(n + 1)}>{n}</button>;
}
```

ตัวอย่างสาธิตแนวคิด ไม่ใช่ไฟล์แอปที่พร้อม deploy; ต้องเติม types/imports, error boundaries และการทดสอบตาม project setup

## จุดพลาดและข้อควรระวัง

อย่าส่ง secret/API key ไปยัง client props หรือ environment ที่ expose; อย่าคิดว่าซ่อนปุ่มเท่ากับป้องกัน endpoint; ตรวจ framework/version เพราะ deployment และ Server Function behavior เป็น framework concern

## แนวทางใช้งาน

วาง client boundary เล็กเท่าที่จำเป็น, ดึงข้อมูล server-side ใกล้ route, ตรวจ authz ใน server action/handler ทุกครั้ง และเข้าใจ caching/revalidation ของ framework

## ความสัมพันธ์

[[React Rendering Model]] · [[Next.js with TypeScript]] · [[OAuth-2.0]] · [[HTTP-Authentication]] · [[React Router Framework]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://react.dev/reference/rsc/server-components)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง
