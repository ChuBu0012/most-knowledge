---
title: "Bun"
type: technology
domain: backend
technology: "Bun"
level: beginner-to-advanced
tags: [technical-knowledge, backend, bun]
status: overview
last_verified: 2026-11-20
sources:
  - https://bun.sh/docs
  - https://bun.sh/blog
---

# Bun

## Overview

JavaScript runtime และ toolkit รวม runtime, package manager, test runner และ bundler

## เลือกใช้เมื่อ

ต้องการ runtime/toolchain แบบรวม หรือทดลอง ecosystem ที่เร็วและครบในตัว

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

[[JavaScript]] · [[Hono]] · [[Vitest]]

## แหล่งข้อมูลและการตรวจสอบ

- [เอกสารทางการ](https://bun.sh/docs)
- [ข่าว/รุ่น/มาตรฐาน](https://bun.sh/blog)
- ตรวจลิงก์และสถานะเอกสารเมื่อ **2026-11-20**; หน้านี้ไม่ได้ pin patch version เพราะเอกสารต้นทางอัปเดตต่อเนื่อง

## อ่านเนื้อหาออฟไลน์

หัวข้อเหล่านี้อธิบายแนวคิดและการตัดสินใจที่เกี่ยวข้อง โดยเนื้อหาสำคัญอยู่ใน Vault ไม่ต้องเปิดเว็บเพื่ออ่านพื้นฐาน:

[[JavaScript Execution Model]] · [[JavaScript Modules]] · [[HTTP Request Lifecycle]]

## Update snapshot — 2026-11-20

Bun 1.4.4 เป็น patch ล่าสุดที่ตรวจ; 1.4 มี HTTP/2 ใน `Bun.serve`; 1.4.4 แก้ compile-cache shutdown regression. Bun APIs เข้ากันได้กับ Node ในระดับต่างกัน ให้ทดสอบ native modules, TLS และ graceful shutdown.

## แนวคิดและคู่มือภายใน Vault

[[JavaScript Execution Model]] · [[JavaScript Modules]] · [[HTTP Request Lifecycle]] · [[Technical-Knowledge/00-Home/Recent-Updates|สรุปอัปเดตทั้งหมด]]


## คำสั่งและสูตรใช้งาน

[[Bun Recipes]] — เริ่มต้น, routes/handlers, validation, errors และการรัน

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
