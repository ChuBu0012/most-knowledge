---
title: "Vite Development and Production Builds"
type: concept
domain: vite
level: intermediate
tags: [vite, bundling, frontend]
status: researched
last_verified: 2026-11-20
sources:
  - https://vite.dev/guide/why.html
---

# Vite Development and Production Builds

## Overview

Vite ใช้ dev server ที่เสิร์ฟ source modules แบบ ESM และทำ production build ผ่าน bundler เพื่อสร้าง assets ที่ optimize แล้ว

## กลไกและแนวคิดหลัก

ใน dev browser ขอ module ตาม import graph; Vite แปลง TypeScript/JSX/CSS และ plugin hooks ระหว่าง request. Production build ต้องจัด chunking, asset hashing, dynamic imports และ base path. Vite ไม่ได้ type-check TypeScript ให้โดยอัตโนมัติ

## ตัวอย่าง

```typescript
// vite.config.ts
import { defineConfig } from 'vite';
export default defineConfig({
  server: { strictPort: true },
});
```

ตัวอย่างสาธิตแนวคิด ไม่ใช่ไฟล์แอปที่พร้อม deploy; ต้องเติม types/imports, error boundaries และการทดสอบตาม project setup

## จุดพลาดและข้อควรระวัง

dev server เปิด network interface ภายนอกได้ถ้ากำหนด host; env ที่ prefix เปิดเผยต่อ browser เป็น public; plugin compatibility และ Node engine เปลี่ยนตาม major - ตรวจ migration notes ก่อน upgrade

## แนวทางใช้งาน

แยก secret env server-side, ใช้ `vite build` เป็น gate ใน pipeline และทดสอบ deploy ใต้ base path/hosting จริง ไม่พึ่ง dev behavior

## ความสัมพันธ์

[[JavaScript Modules]] · [[Vitest]] · [[React]] · [[Vue]] · [[SvelteKit]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://vite.dev/guide/why.html)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
