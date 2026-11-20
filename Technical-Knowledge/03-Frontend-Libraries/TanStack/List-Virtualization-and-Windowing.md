---
title: "List Virtualization and Windowing"
type: concept
domain: tanstack virtual
level: intermediate
tags: [virtualization, performance, ui]
status: researched
last_verified: 2026-11-20
sources:
  - https://tanstack.com/virtual/latest/docs/introduction
---

# List Virtualization and Windowing

## Overview

Windowing render เฉพาะ rows/items ที่อยู่ใกล้ viewport พร้อม spacer/positioning เพื่อให้ list ใหญ่มีจำนวน DOM nodes คงที่

## กลไกและแนวคิดหลัก

virtualizer รับ item count, scroll element, estimated/actual sizes และ viewport; คำนวณช่วง visible indexes พร้อม overscan. Variable-height rows ต้องวัด element หลัง render และ update size cache. Virtualization ลด DOM/layout cost แต่ไม่ได้ลดต้นทุนการดึง/ประมวลผลข้อมูลทั้งหมด

## ตัวอย่าง

```tsx
const virtualizer = useVirtualizer({
  count: rows.length,
  getScrollElement: () => parentRef.current,
  estimateSize: () => 36,
  overscan: 8,
});
```

ตัวอย่างเป็น schematic; adapter/package imports และ API ต้องตรงกับ version ที่ใช้จริง

## จุดพลาดและข้อควรระวัง

การใช้ index เป็น stable key เมื่อข้อมูล reorder ทำให้ measurements/state ไปผิด row; scroll-to-index ต้องรู้ size/measurement; ตารางที่มี sticky header, keyboard navigation และ screen readers ต้องออกแบบ semantic/aria behavior เพิ่ม

## แนวทางปฏิบัติ

วัดจริงก่อน virtualize; ตั้ง overscan ตาม scroll velocity; รักษา stable item identity; ทดสอบ keyboard, focus, zoom และ screen reader; ใช้ pagination ถ้าต้องการลด data transfer ด้วย

## ความสัมพันธ์

[[TanStack-Virtual]] · [[TanStack-Table]] · [[TanStack Query Cache Lifecycle]] · [[Playwright Locators and Auto-Waiting]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://tanstack.com/virtual/latest/docs/introduction)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง
