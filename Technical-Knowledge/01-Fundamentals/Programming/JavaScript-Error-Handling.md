---
title: "JavaScript Error Handling"
type: concept
domain: javascript
level: intermediate
tags:
  - javascript
  - errors
status: researched
last_verified: 2026-11-20
sources:
  - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Control_flow_and_error_handling
---

# JavaScript Error Handling

## Overview

error handling แบ่ง failure ที่คาดไว้ให้ caller จัดการ ออกจาก bug ที่ควรพบระหว่างพัฒนา

## กลไกและแนวคิดหลัก

throw ข้าม call stack จนพบ catch; Promise rejection ทำงานตาม chain และจะกลายเป็น unhandled rejection หากไม่มี handler ที่เหมาะสม สร้าง Error พร้อมข้อความที่ actionable และรักษา cause ไว้เมื่อแปลงระดับ error

## ตัวอย่าง

```javascript
try {
  await saveOrder(order);
} catch (cause) {
  throw new Error("บันทึกคำสั่งซื้อไม่สำเร็จ", { cause });
}
```

ตัวอย่างแสดงแนวคิดหลักเท่านั้น ให้เพิ่มการตรวจ input, resource cleanup และ error handling ตามบริบทก่อนใช้ production

## จุดพลาดและข้อควรระวัง

อย่า catch แล้วคืน `null`/ค่า default โดยไม่บอก caller เพราะแยก failure จากข้อมูลปกติไม่ได้ อย่าส่งรายละเอียดภายใน, token หรือข้อมูลส่วนบุคคลไปยัง client log; จัดการ error ที่ boundary ของ request/UI

## แนวทางใช้งาน

แบ่ง validation errors, transient dependency errors และ programming errors เพราะ retry/ข้อความผู้ใช้/การแจ้งเตือนต่างกัน

## ความสัมพันธ์

- Related: [[JavaScript Promises]] · [[FastAPI]] · [[Gin]] · [[Vitest]]
- เปิดภาพรวมหมวด: [[Technology-Index]] · [[Knowledge-Map]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Control_flow_and_error_handling)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง
