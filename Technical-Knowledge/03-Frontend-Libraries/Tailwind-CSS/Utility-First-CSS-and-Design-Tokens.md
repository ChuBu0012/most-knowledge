---
title: "Utility-First CSS and Design Tokens"
type: concept
domain: tailwind css
level: intermediate
tags: [css, design-system, accessibility]
status: researched
last_verified: 2026-11-20
sources:
  - https://tailwindcss.com/docs/theme
---

# Utility-First CSS and Design Tokens

## Overview

utility-first CSS เขียน style จากชุด class เล็ก ๆ ใน markup ส่วน design tokens ทำให้สี, spacing, type และ radius มีค่ากลางสม่ำเสมอ

## กลไกและแนวคิดหลัก

Tailwind scan source files แล้ว generate เฉพาะ utility ที่พบ; responsive/state variants เป็น selector ที่ compile ได้. ใน v4 CSS-first theme variables ใช้กำหนด token และ custom utility. Component library เช่น DaisyUI เติม semantic component class; headless primitive เช่น Reka UI เติม behavior/accessibility แต่ให้ผู้ใช้กำหนด style

## ตัวอย่าง

```tsx
<button class="bg-blue-700 px-4 py-2 text-white hover:bg-blue-800 focus-visible:outline-2">
  Save
</button>
```

ตัวอย่างเป็น schematic; adapter/package imports และ API ต้องตรงกับ version ที่ใช้จริง

## จุดพลาดและข้อควรระวัง

dynamic class string เช่น `bg-${color}-500` อาจไม่ถูกค้นพบตอน build; ใช้ mapping ไปยัง literal classes หรือ safelist ตาม tool version. Utility ไม่รับประกัน contrast/focus/accessibility; class ยาวอาจซ้ำโดยไม่มี component boundary

## แนวทางปฏิบัติ

จัด tokens ตาม semantic intent (surface/text/action) แทนชื่อสี; ใช้ variants สำหรับ responsive/focus/reduced motion; ตรวจ keyboard/contrast และ production CSS output

## ความสัมพันธ์

[[Tailwind-CSS]] · [[DaisyUI]] · [[Reka-UI]] · [[Vite Development and Production Builds]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://tailwindcss.com/docs/theme)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง
