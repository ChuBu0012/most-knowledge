---
title: "Unit Integration and End-to-End Tests"
type: concept
domain: testing
level: intermediate-to-advanced
tags: [testing, quality, verification]
status: researched
last_verified: 2026-11-20
sources:
  - https://martinfowler.com/articles/practical-test-pyramid.html
---

# Unit Integration and End-to-End Tests

## Overview

test levels ต่างกันตามขอบเขต dependency ที่จริง: unit ทดสอบ logic แคบ, integration ทดสอบ collaboration จริง, end-to-end ทดสอบ journey ผ่านระบบประกอบ

## กลไกและแนวคิดหลัก

unit tests ให้ feedback เร็วแต่ mock มากเกินอาจยืนยัน behavior ปลอม. Integration ใช้ database/protocol จริงหรือ test container เพื่อตรวจ contract. Browser E2E ช้ากว่าและ flaky ได้ จึงควรเลือก critical workflows ไม่ใช่ทุก permutation. Test pyramid เป็น heuristic เรื่องจำนวน/ต้นทุน ไม่ใช่กฎตายตัว

## ตัวอย่าง

```text
// Arrange → Act → Assert
const result = calculateTotal([{ price: 10, qty: 2 }]);
expect(result).toBe(20);
```

ตัวอย่างเป็น schematic ที่สื่อหลักการ; ตรวจ syntax และ config ให้ตรงกับ version/runtime ที่ใช้งานก่อนนำไป deploy

## จุดพลาดและข้อควรระวัง

อย่าทดสอบ implementation details เช่น private function call count โดยไม่จำเป็น; หลีกเลี่ยง shared mutable fixtures และ sleep-based waits; flaky test ต้องหา race/environment cause ไม่ใช่เพิ่ม retry อย่างเดียว

## แนวทางปฏิบัติ

ผูกแต่ละ test กับ risk/behavior, ใช้ deterministic data, แยก test environments และเก็บ trace/log เมื่อ browser flow ล้ม

## ความสัมพันธ์

[[Vitest]] · [[Playwright]] · [[Go Testing]] · [[Database-Transactions]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://martinfowler.com/articles/practical-test-pyramid.html)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง
