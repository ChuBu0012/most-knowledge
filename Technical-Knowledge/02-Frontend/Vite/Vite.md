---
title: "Vite"
type: technology
domain: frontend
technology: "Vite"
level: beginner-to-advanced
tags: [technical-knowledge, frontend, vite]
status: overview
last_verified: 2026-11-20
sources:
  - https://vite.dev/guide/
  - https://vite.dev/blog/
  - https://vite.dev/releases
---

# Vite

## Overview

เครื่องมือ dev server และ build สำหรับ frontend โดยใช้ native ESM ระหว่างพัฒนาและ bundling ตอน production

## เลือกใช้เมื่อ

SPA หรือ library frontend ที่ต้องการ feedback loop เร็วและยืดหยุ่น

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

[[Vitest]] · [[React]] · [[Vue]] · [[SvelteKit]]

## แหล่งข้อมูลและการตรวจสอบ

- [เอกสารทางการ](https://vite.dev/guide/)
- [ข่าว/รุ่น/มาตรฐาน](https://vite.dev/blog/)
- ตรวจลิงก์และสถานะเอกสารเมื่อ **2026-11-20**; หน้านี้ไม่ได้ pin patch version เพราะเอกสารต้นทางอัปเดตต่อเนื่อง

## อ่านเนื้อหาออฟไลน์

หัวข้อเหล่านี้อธิบายแนวคิดและการตัดสินใจที่เกี่ยวข้อง โดยเนื้อหาสำคัญอยู่ใน Vault ไม่ต้องเปิดเว็บเพื่ออ่านพื้นฐาน:

[[JavaScript Modules]] · [[Vite Development and Production Builds]]

## Update snapshot — 2026-11-20

Vite 8.3 release train; Vite 8 รวม bundling ผ่าน Rolldown และต้องใช้ Node 20.19+ หรือ 22.12+. ตรวจ [supported releases](https://vite.dev/releases) และ plugin compatibility. TypeScript transpilation ไม่ใช่การ type-check; รัน checker แยก.

## แนวคิดและคู่มือภายใน Vault

[[Vite Development and Production Builds]] · [[JavaScript Modules]] · [[Vitest]] · [[Technical-Knowledge/00-Home/Recent-Updates|สรุปอัปเดตทั้งหมด]]
