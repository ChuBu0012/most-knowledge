---
title: "Vitest"
type: technology
domain: testing
technology: "Vitest"
level: beginner-to-advanced
tags: [technical-knowledge, testing, vitest]
status: overview
last_verified: 2026-11-20
sources:
  - https://vitest.dev/guide/
  - https://vitest.dev/blog/
---

# Vitest

## Overview

test runner สำหรับ JavaScript/TypeScript ผสาน Vite transform/config และมี API คุ้นเคย

## เลือกใช้เมื่อ

โปรเจกต์ Vite ต้องการ unit/component testing ที่ใช้ config ร่วม

## ทำความเข้าใจให้ถูกก่อนเริ่ม

- หน้านี้เป็นแผนที่เริ่มต้น ไม่ใช่คู่มือ API ครบชุด ให้ยึดเอกสารทางการตามเวอร์ชันที่ติดตั้งจริง
- เวอร์ชันและความเข้ากันได้เปลี่ยนได้ ตรวจ release notes/compatibility ก่อนเริ่มโปรเจกต์หรืออัปเกรด
- เริ่มจากแนวคิดและตัวอย่างเล็ก แล้วค่อยนำไปผสานกับแอปจริง; อย่าคัดลอก config โดยไม่เข้าใจ runtime และ deployment target

## เส้นทางเรียนรู้

1. อ่าน Getting Started และเข้าใจ model หลักของเครื่องมือนี้
2. ทดลองตัวอย่างขั้นต่ำในโปรเจกต์แยก พร้อมบันทึก runtime, dependency และเวอร์ชัน
3. ศึกษาการจัดการ error, testing, security และ production configuration ที่เกี่ยวข้อง
4. เปรียบเทียบ trade-offs กับทางเลือกที่ลิงก์ด้านล่างก่อนยึดเป็นมาตรฐานของโปรเจกต์

## ความสัมพันธ์กับเรื่องอื่น

[[Vite]] · [[Playwright]] · [[Go Testing]]

## แหล่งข้อมูลและการตรวจสอบ

- [เอกสารทางการ](https://vitest.dev/guide/)
- [ข่าว/รุ่น/มาตรฐาน](https://vitest.dev/blog/)
- ตรวจลิงก์และสถานะเอกสารเมื่อ **2026-11-20**; หน้านี้ไม่ได้ pin patch version เพราะเอกสารต้นทางอัปเดตต่อเนื่อง

## อ่านเนื้อหาออฟไลน์

หัวข้อเหล่านี้อธิบายแนวคิดและการตัดสินใจที่เกี่ยวข้อง โดยเนื้อหาสำคัญอยู่ใน Vault ไม่ต้องเปิดเว็บเพื่ออ่านพื้นฐาน:

[[Unit Integration and End-to-End Tests]] · [[Vite Development and Production Builds]]

## Update snapshot — 2026-11-20

Vitest 5.1 เป็น release train ปัจจุบัน; Vite >=6.4 และ Node >=22.12. `clearMocks` เปิดเป็นค่าเริ่มต้นและ Vite เป็น peer dependency ชัดเจน (Yarn ต้องเพิ่มเอง). อ่าน [migration guide](https://vitest.dev/guide/migration/) ก่อน major upgrade.

## แนวคิดและคู่มือภายใน Vault

[[Unit Integration and End-to-End Tests]] · [[Vite Development and Production Builds]] · [[Technical-Knowledge/00-Home/Recent-Updates|สรุปอัปเดตทั้งหมด]]


## คำสั่งและสูตรใช้งาน

[[Vitest Recipes]] — task-first walkthrough สำหรับการใช้งานจริง

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
