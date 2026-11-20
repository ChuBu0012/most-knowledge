---
title: "JavaScript Modules"
type: concept
domain: javascript
level: intermediate
tags:
  - javascript
  - modules
status: researched
last_verified: 2026-11-20
sources:
  - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules
---

# JavaScript Modules

## Overview

ES modules แบ่งโปรแกรมเป็นไฟล์ที่ export/import bindings อย่างชัดเจน ช่วยควบคุม dependency และเปิดโอกาสให้ tree-shaking

## กลไกและแนวคิดหลัก

`import`/`export` เป็น static syntax ที่ loader วิเคราะห์ dependency graph ได้ก่อน execute. ESM มี live bindings, module scope และประเมินแต่ละ module ครั้งเดียวต่อ module graph โดยทั่วไป CommonJS ใช้ `require` แบบ runtime และยังพบใน ecosystem Node.js

## ตัวอย่าง

```javascript
// math.js
export function add(a, b) { return a + b; }

// app.js
import { add } from "./math.js";
console.log(add(2, 3));
```

ตัวอย่างแสดงแนวคิดหลักเท่านั้น ให้เพิ่มการตรวจ input, resource cleanup และ error handling ตามบริบทก่อนใช้ production

## จุดพลาดและข้อควรระวัง

อย่าสับสน default export กับ named export; path resolution, file extension และ interop แตกต่างตาม browser, Node.js, Bun และ bundler ตรวจ `package.json` (`type`, `exports`) และ config ของ toolchain ก่อนเปลี่ยน module format

## แนวทางใช้งาน

ใน library ให้กำหนด public exports ผ่าน package exports map; หลีกเลี่ยง circular dependencies ที่ทำให้ initialization order สับสน

## ความสัมพันธ์

- Related: [[TypeScript]] · [[Vite]] · [[Node.js]] · [[Bun]]
- เปิดภาพรวมหมวด: [[Technology-Index]] · [[Knowledge-Map]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง
