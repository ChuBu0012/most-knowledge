---
title: "Browser Form State"
type: concept
domain: forms
level: intermediate
tags: [forms, validation, frontend]
status: researched
last_verified: 2026-11-20
sources:
  - https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms
---

# Browser Form State

## Overview

ฟอร์มมี state มากกว่าค่า input: touched/dirty, validation, submission, server errors และสถานะระหว่างส่ง

## กลไกและแนวคิดหลัก

เลือก uncontrolled inputs เมื่อเหมาะเพื่อลด re-render หรือ controlled state เมื่อ UI ต้องตอบสนองต่อค่าทุกการเปลี่ยน; schema validation ควรทำซ้ำ server-side เพราะ client แก้ไข/ข้ามได้. แยก client validation เพื่อ UX ออกจาก server validation ที่เป็น authority

## ตัวอย่าง

```svelte
// แนวคิด: parse payload ก่อน mutation
const result = FormSchema.safeParse(formValues);
if (!result.success) return showErrors(result.error);
await saveOnServer(result.data);
```

ตัวอย่างสาธิตแนวคิด ไม่ใช่ไฟล์แอปที่พร้อม deploy; ต้องเติม types/imports, error boundaries และการทดสอบตาม project setup

## จุดพลาดและข้อควรระวัง

อย่าใช้ client validation เป็น security control; อย่าส่ง duplicate submits ระหว่าง pending; ข้อผิดพลาดจาก server อาจไม่ตรง field และต้องคงไว้เป็น form-level error

## แนวทางใช้งาน

เลือก React Hook Form สำหรับ ecosystem React ที่ mature, VeeValidate สำหรับ Vue, TanStack Form เมื่ออยากได้ headless cross-framework primitives; ตรวจ stable/beta API ก่อน adopt

## ความสัมพันธ์

[[Zod Runtime Validation]] · [[React-Hook-Form]] · [[VeeValidate]] · [[TanStack-Form]] · [[Playwright]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง
