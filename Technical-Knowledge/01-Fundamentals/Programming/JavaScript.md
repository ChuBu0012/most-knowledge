---
title: "JavaScript"
type: technology
domain: fundamentals
technology: "JavaScript"
level: beginner-to-advanced
tags: [technical-knowledge, fundamentals, programming]
status: overview
last_verified: 2026-11-20
sources:
  - https://developer.mozilla.org/en-US/docs/Web/JavaScript
  - https://tc39.es/ecma262/
---

# JavaScript

## Overview

ภาษาโปรแกรมหลักของเว็บ ใช้สร้างพฤติกรรมหน้าเว็บและทำงานบน server ผ่าน runtime เช่น Node.js หรือ Bun

## เลือกใช้เมื่อ

ต้องการพัฒนาบนเว็บหรือใช้ ecosystem JavaScript

## ทำความเข้าใจให้ถูกก่อนเริ่ม

- หน้านี้เป็นแผนที่เริ่มต้น ไม่ใช่คู่มือ API ครบชุด ให้ยึดเอกสารทางการตามเวอร์ชันที่ติดตั้งจริง
- เวอร์ชันและความเข้ากันได้เปลี่ยนได้ ตรวจ release notes/compatibility ก่อนเริ่มโปรเจกต์หรืออัปเกรด
- เริ่มจากแนวคิดและตัวอย่างเล็ก แล้วค่อยนำไปผสานกับแอปจริง; อย่าคัดลอก config โดยไม่เข้าใจ runtime และ deployment target

## เส้นทางเรียนรู้

1. อ่าน Getting Started และเข้าใจ model หลักของเครื่องมือนี้
2. ทดลองตัวอย่างขั้นต่ำในโปรเจกต์แยก พร้อมบันทึก runtime, dependency และเวอร์ชัน
3. ศึกษาการจัดการ error, testing, security และ production configuration ที่เกี่ยวข้อง
4. เปรียบเทียบ trade-offs กับทางเลือกที่ลิงก์ด้านล่างก่อนยึดเป็นมาตรฐานของโปรเจกต์

## Update snapshot — 2026-11-20

JavaScript standards work continues through TC39; use the living ECMAScript specification and MDN compatibility data for features. The durable model remains lexical scope, jobs/microtasks, promises, modules, and explicit runtime validation at IO boundaries.

แหล่งยืนยัน snapshot: - [https://tc39.es/ecma262/](https://tc39.es/ecma262/)
- [https://developer.mozilla.org/en-US/docs/Web/JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

## ความสัมพันธ์กับเรื่องอื่น

[[TypeScript]] · [[React]] · [[Node.js]]

## แหล่งข้อมูลและการตรวจสอบ

- [เอกสารทางการ](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
- [ข่าว/รุ่น/มาตรฐาน](https://tc39.es/ecma262/)
- ตรวจลิงก์และสถานะเอกสารเมื่อ **2026-11-20**; หน้านี้ไม่ได้ pin patch version เพราะเอกสารต้นทางอัปเดตต่อเนื่อง

## อ่านเนื้อหาออฟไลน์

หัวข้อเหล่านี้อธิบายแนวคิดและการตัดสินใจที่เกี่ยวข้อง โดยเนื้อหาสำคัญอยู่ใน Vault ไม่ต้องเปิดเว็บเพื่ออ่านพื้นฐาน:

[[JavaScript Execution Model]] · [[JavaScript Promises]] · [[JavaScript Closures]] · [[JavaScript Modules]] · [[JavaScript Error Handling]]


## คำสั่งและสูตรใช้งาน

[[JavaScript Recipes]] — ค้น API/คำสั่งจากงานที่ต้องทำ พร้อมตัวอย่างและข้อควรระวัง

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
