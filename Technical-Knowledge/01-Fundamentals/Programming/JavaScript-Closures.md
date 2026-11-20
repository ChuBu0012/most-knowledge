---
title: "JavaScript Closures"
type: concept
domain: javascript
level: intermediate
tags:
  - javascript
  - functions
status: researched
last_verified: 2026-11-20
sources:
  - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures
---

# JavaScript Closures

## Overview

closure คือฟังก์ชันพร้อม lexical environment ที่สร้างฟังก์ชันนั้น ทำให้ฟังก์ชันเก็บการเข้าถึงค่าจากขอบเขตเดิมได้

## กลไกและแนวคิดหลัก

JavaScript resolve identifier จาก lexical scope ตอนเขียนโค้ด ไม่ใช่จากตำแหน่งที่เรียกฟังก์ชัน ค่าใน closure เป็น binding; ถ้า binding เปลี่ยนภายหลัง ฟังก์ชันจะเห็นค่าปัจจุบันของ binding นั้น

## ตัวอย่าง

```javascript
function makeCounter() {
  let count = 0;
  return () => ++count;
}
const next = makeCounter();
next(); // 1
next(); // 2
```

ตัวอย่างแสดงแนวคิดหลักเท่านั้น ให้เพิ่มการตรวจ input, resource cleanup และ error handling ตามบริบทก่อนใช้ production

## จุดพลาดและข้อควรระวัง

closure ใช้ทำ encapsulation, callbacks และ hooks ได้ แต่ callback ที่อยู่ยาวกว่าหน้าจออาจเก็บข้อมูล/DOM ใหญ่ไว้ใน memory หรืออ่าน state เก่าหาก dependency/callback lifecycle ไม่ถูกต้อง ใน loop ใช้ `let` เพื่อให้แต่ละ iteration มี binding ของตัวเอง

## แนวทางใช้งาน

ใช้ closure เพื่อซ่อน implementation detail ขนาดเล็ก อย่าใช้เป็น global state แฝงที่ไม่มีเจ้าของและ lifecycle ชัดเจน

## ความสัมพันธ์

- Related: [[React Rendering Model]] · [[State Management Concepts]] · [[TypeScript Generics]]
- เปิดภาพรวมหมวด: [[Technology-Index]] · [[Knowledge-Map]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง
