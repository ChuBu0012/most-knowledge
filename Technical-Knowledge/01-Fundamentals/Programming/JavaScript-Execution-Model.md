---
title: "JavaScript Execution Model"
type: concept
domain: javascript
level: intermediate
tags:
  - javascript
  - runtime
status: researched
last_verified: 2026-11-20
sources:
  - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Event_loop
---

# JavaScript Execution Model

## Overview

การเข้าใจ execution model ช่วยอธิบายว่าทำไมโค้ด synchronous จึงบล็อกงานอื่น และทำไม async callback จึงทำงานภายหลัง

## กลไกและแนวคิดหลัก

JavaScript ทำงานบน call stack เดียวต่อ execution context หนึ่ง งานเรียกฟังก์ชันจะ push frame ลง stack และคืนผลเมื่อ pop ออกมา Browser หรือ runtime เติมความสามารถนอกภาษา เช่น timer, file I/O และ network ส่วน event loop คอยนำ callback ที่พร้อมกลับเข้ามาทำงานเมื่อ stack ว่าง

## ตัวอย่าง

```javascript
console.log("A");
setTimeout(() => console.log("timer"), 0);
Promise.resolve().then(() => console.log("promise"));
console.log("B");
// A, B, promise, timer
```

ตัวอย่างแสดงแนวคิดหลักเท่านั้น ให้เพิ่มการตรวจ input, resource cleanup และ error handling ตามบริบทก่อนใช้ production

## จุดพลาดและข้อควรระวัง

Promise reactions อยู่ใน microtask queue และถูกประมวลผลหลัง synchronous code จบ ก่อน timer task รอบถัดไป การตั้ง timeout เป็น 0 ไม่ได้แปลว่ารันทันที และ long task จะหยุดการตอบสนองของ UI ทั้งหมด

## แนวทางใช้งาน

อย่ามอง asynchronous ว่าเท่ากับ parallel execution; event loop จัดลำดับ continuation ส่วน CPU-heavy computation ยังบล็อก thread เดิม ใช้ Worker เมื่อจำเป็นต้องย้ายงานคำนวณ

## ความสัมพันธ์

- Related: [[JavaScript Promises]] · [[JavaScript Modules]] · [[HTTP]] · [[Node.js]]
- เปิดภาพรวมหมวด: [[Technology-Index]] · [[Knowledge-Map]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Event_loop)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง
