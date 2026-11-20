---
title: "TypeScript Structural Types"
type: concept
domain: typescript
level: intermediate
tags:
  - typescript
  - types
status: researched
last_verified: 2026-11-20
sources:
  - https://www.typescriptlang.org/docs/handbook/type-compatibility.html
---

# TypeScript Structural Types

## Overview

ระบบ structural typing ตัดสินความเข้ากันได้จากรูปร่างของสมาชิก ไม่ใช่ชื่อ class/type ที่ประกาศ

## กลไกและแนวคิดหลัก

ถ้า object มี property และ signature ที่จำเป็น ก็ assign เข้า target type ได้ หลักนี้เหมาะกับ object literals และ API ที่ composable แต่ทำให้ค่าคนละ domain ที่มี primitive เดียวกัน เช่น UserId กับ OrderId ดูสับสน

## ตัวอย่าง

```javascript
type User = { id: string; name: string };
const record = { id: "u1", name: "Mali", internal: true };
const user: User = record; // มีสมาชิกที่ต้องใช้ครบ
```

ตัวอย่างแสดงแนวคิดหลักเท่านั้น ให้เพิ่มการตรวจ input, resource cleanup และ error handling ตามบริบทก่อนใช้ production

## จุดพลาดและข้อควรระวัง

excess-property checking ของ object literal ตรง ๆ เป็น heuristic ไม่ได้เปลี่ยนระบบให้ nominal อย่าใช้ `string` ตัวเดียวแทน identifier สำคัญหลายชนิด; ใช้ branded type หรือ wrapper เมื่อการสลับค่าจะก่อ bug

## แนวทางใช้งาน

ออกแบบ public contracts จาก data ที่ผู้ใช้ต้องใช้จริง; หลีกเลี่ยง interface ขนาดใหญ่ที่บังคับ implement รายละเอียดไม่เกี่ยวข้อง

## ความสัมพันธ์

- Related: [[TypeScript Generics]] · [[React with TypeScript]] · [[OpenAPI]]
- เปิดภาพรวมหมวด: [[Technology-Index]] · [[Knowledge-Map]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://www.typescriptlang.org/docs/handbook/type-compatibility.html)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
