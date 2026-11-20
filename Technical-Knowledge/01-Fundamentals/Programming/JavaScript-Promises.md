---
title: "JavaScript Promises"
type: concept
domain: javascript
level: intermediate
tags:
  - javascript
  - async
status: researched
last_verified: 2026-11-20
sources:
  - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises
---

# JavaScript Promises

## Overview

Promise แทนผลลัพธ์ของงานที่ยังไม่เสร็จหรืออาจล้มเหลว ช่วยต่อ asynchronous computation โดยไม่ซ้อน callback

## กลไกและแนวคิดหลัก

Promise มีสถานะ pending, fulfilled หรือ rejected และเปลี่ยนจาก pending ได้เพียงครั้งเดียว `.then()` สร้าง Promise ใหม่ ทำให้ chain แปลงค่าและส่งต่อ error ได้ `async` function คืน Promise เสมอ; `await` พักเฉพาะ continuation ของฟังก์ชันนั้น ไม่ได้หยุด event loop

## ตัวอย่าง

```javascript
async function loadUser(id) {
  const response = await fetch(`/api/users/${id}`);
  if (!response.ok) throw new Error(`HTTP ${response.status}`);
  return response.json();
}

try {
  const user = await loadUser("42");
} catch (error) {
  // แสดง/ส่งต่อ error ตามขอบเขตที่รับผิดชอบ
}
```

ตัวอย่างแสดงแนวคิดหลักเท่านั้น ให้เพิ่มการตรวจ input, resource cleanup และ error handling ตามบริบทก่อนใช้ production

## จุดพลาดและข้อควรระวัง

`fetch` reject เมื่อ network ล้มเหลว แต่ HTTP 404/500 ยัง resolve เป็น Response; จึงต้องตรวจ `response.ok` เอง อย่ากลืน error ด้วย catch ว่าง และอย่า `await` งานอิสระทีละตัวถ้าสามารถใช้ `Promise.all` ได้

## แนวทางใช้งาน

ใช้ `Promise.all` เมื่องานทั้งหมดจำเป็นต้องสำเร็จ, `Promise.allSettled` เมื่อต้องการผลแยกแต่ละงาน และกำหนด timeout/cancellation ที่ขอบเขต I/O ผ่าน `AbortSignal`

## ความสัมพันธ์

- Related: [[JavaScript Execution Model]] · [[HTTP]] · [[React Rendering Model]] · [[TanStack-Query]]
- เปิดภาพรวมหมวด: [[Technology-Index]] · [[Knowledge-Map]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง
