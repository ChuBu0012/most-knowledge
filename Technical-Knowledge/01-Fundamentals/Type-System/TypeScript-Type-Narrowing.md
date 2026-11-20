---
title: "TypeScript Type Narrowing"
type: concept
domain: typescript
level: intermediate
tags:
  - typescript
  - type-system
status: researched
last_verified: 2026-11-20
sources:
  - https://www.typescriptlang.org/docs/handbook/2/narrowing.html
---

# TypeScript Type Narrowing

## Overview

narrowing ใช้ control flow และการตรวจ runtime ลด union type ให้แคบลงในแต่ละ branch

## กลไกและแนวคิดหลัก

TypeScript ตรวจโปรแกรมแบบ structural และใช้ guard เช่น `typeof`, `in`, equality, discriminant property และ user-defined predicates เพื่อคำนวณ type ที่ปลอดภัยขึ้น แต่ type ถูกลบตอน compile; ข้อมูลภายนอกจึงต้อง validate ที่ runtime

## ตัวอย่าง

```javascript
type Result<T> =
  | { ok: true; value: T }
  | { ok: false; error: Error };

function unwrap<T>(result: Result<T>): T {
  if (result.ok) return result.value;
  throw result.error;
}
```

ตัวอย่างแสดงแนวคิดหลักเท่านั้น ให้เพิ่มการตรวจ input, resource cleanup และ error handling ตามบริบทก่อนใช้ production

## จุดพลาดและข้อควรระวัง

ใช้ discriminated union แทน flag หลายตัวที่ขัดกันได้ (`isLoading`, `hasError`, `data?`) และหลีกเลี่ยง `as SomeType` เพื่อบังคับ compiler ให้เชื่อโดยไม่ตรวจข้อมูลจริง

## แนวทางใช้งาน

เริ่มจาก type ที่แคบและขยายเมื่อจำเป็น; ใช้ `unknown` สำหรับ input ที่ยังไม่พิสูจน์ แล้ว narrow ผ่าน schema เช่น [[Zod]]

## ความสัมพันธ์

- Related: [[TypeScript Generics]] · [[Zod]] · [[React with TypeScript]] · [[FastAPI]]
- เปิดภาพรวมหมวด: [[Technology-Index]] · [[Knowledge-Map]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
