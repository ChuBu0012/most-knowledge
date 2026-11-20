---
title: "Zod Runtime Validation"
type: concept
domain: zod
level: intermediate
tags: [zod, validation, typescript]
status: researched
last_verified: 2026-11-20
sources:
  - https://zod.dev/basics
---

# Zod Runtime Validation

## Overview

Zod schema ใช้ parse ข้อมูลที่ type checker ไม่สามารถรับรองตอน runtime และสร้าง TypeScript type จาก schema ได้

## กลไกและแนวคิดหลัก

`parse` คืนข้อมูลที่ผ่านการตรวจหรือ throw; `safeParse` คืน discriminated union สำหรับจัดการ error โดยไม่ใช้ exception. Schema สามารถ transform/coerce ได้ แต่ควรระบุให้ชัดเพราะ output type อาจต่างจาก input. Validation ที่ขอบเขต trust เช่น request, env/config และ local storage สำคัญที่สุด

## ตัวอย่าง

```typescript
const User = z.object({
  id: z.string().uuid(),
  email: z.email(),
});
type User = z.infer<typeof User>;
const parsed = User.safeParse(input);
```

ตัวอย่างสาธิตแนวคิด ไม่ใช่ไฟล์แอปที่พร้อม deploy; ต้องเติม types/imports, error boundaries และการทดสอบตาม project setup

## จุดพลาดและข้อควรระวัง

TypeScript type assertion ไม่ตรวจ JSON จริง; อย่า expose raw validation internals ให้ผู้ใช้; coercion อาจเปลี่ยน `""`/`null` เป็นค่าที่ไม่คาดคิด; schema ใหญ่ไม่ควร duplicate server/client โดยไม่ตั้งใจ

## แนวทางใช้งาน

parse ที่ boundary, แยก input/output schema เมื่อ transform, เขียน error mapping ที่เป็นมิตร และใช้ schema ร่วมกับ form/database contracts ตามความเหมาะสม

## ความสัมพันธ์

[[TypeScript Type Narrowing]] · [[React-Hook-Form]] · [[TanStack-Form]] · [[VeeValidate]] · [[OpenAPI]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://zod.dev/basics)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
