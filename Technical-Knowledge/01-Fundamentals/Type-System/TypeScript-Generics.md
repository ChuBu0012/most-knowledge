---
title: "TypeScript Generics"
type: concept
domain: typescript
level: intermediate
tags:
  - typescript
  - generics
status: researched
last_verified: 2026-11-20
sources:
  - https://www.typescriptlang.org/docs/handbook/2/generics.html
---

# TypeScript Generics

## Overview

generics สร้าง function/type ที่ทำงานกับหลายชนิดข้อมูลโดยรักษาความสัมพันธ์ของ input กับ output

## กลไกและแนวคิดหลัก

type parameter แทนชนิดที่ยังไม่รู้ในจุดประกาศ แต่ถูกอนุมานจาก call site ได้ constraint จำกัด operations ที่ทำได้ เช่น `T extends { id: string }` ใช้ generic เมื่อมีความสัมพันธ์ชนิดที่ต้องรักษา ไม่ใช่เพียงทำให้ type ดูซับซ้อน

## ตัวอย่าง

```javascript
function first<T>(items: readonly T[]): T | undefined {
  return items[0];
}
const user = first([{ id: "u1" }]); // { id: string } | undefined
```

ตัวอย่างแสดงแนวคิดหลักเท่านั้น ให้เพิ่มการตรวจ input, resource cleanup และ error handling ตามบริบทก่อนใช้ production

## จุดพลาดและข้อควรระวัง

generic ที่กว้างเกินไปทำให้ error อ่านยากและ API ใช้ยาก อย่าใช้ `any` ใน generic เพราะทำลายความสัมพันธ์ชนิด; ระวัง variance และ type inference ที่เปลี่ยนเมื่อเพิ่ม overload/conditional type

## แนวทางใช้งาน

ตั้งชื่อ type parameters สื่อความหมายเมื่อมีมากกว่าหนึ่งตัว และเริ่มจาก inference ก่อนเพิ่ม explicit type arguments

## ความสัมพันธ์

- Related: [[TypeScript Type Narrowing]] · [[React with TypeScript]] · [[Zod]]
- เปิดภาพรวมหมวด: [[Technology-Index]] · [[Knowledge-Map]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://www.typescriptlang.org/docs/handbook/2/generics.html)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
