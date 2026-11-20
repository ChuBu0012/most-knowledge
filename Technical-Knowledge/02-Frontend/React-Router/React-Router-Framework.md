---
title: "React Router Framework"
type: technology
domain: frontend
technology: "React Router Framework"
level: beginner-to-advanced
tags: [technical-knowledge, frontend, react-router]
status: overview
last_verified: 2026-11-20
sources:
  - https://reactrouter.com/start/framework/installation
  - https://github.com/remix-run/react-router/releases
---

# React Router Framework

## Overview

React Router ใน Framework Mode เชื่อม route modules, data loading/actions และ rendering เข้ากับแอปเว็บ

## เลือกใช้เมื่อ

ต้องการ routing/data mutations แบบ route-centric หรือย้ายจาก Remix

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

[[React]] · [[Hono]] · [[Next.js with TypeScript]]

## แหล่งข้อมูลและการตรวจสอบ

- [เอกสารทางการ](https://reactrouter.com/start/framework/installation)
- [ข่าว/รุ่น/มาตรฐาน](https://github.com/remix-run/react-router/releases)
- ตรวจลิงก์และสถานะเอกสารเมื่อ **2026-11-20**; หน้านี้ไม่ได้ pin patch version เพราะเอกสารต้นทางอัปเดตต่อเนื่อง

## อ่านเนื้อหาออฟไลน์

หัวข้อเหล่านี้อธิบายแนวคิดและการตัดสินใจที่เกี่ยวข้อง โดยเนื้อหาสำคัญอยู่ใน Vault ไม่ต้องเปิดเว็บเพื่ออ่านพื้นฐาน:

[[HTTP Request Lifecycle]] · [[HTTP Semantics and REST]] · [[React Server and Client Components]]

## Update snapshot — 2026-11-20

v8.5.2 (18 Nov 2026) แก้ metadata/navigation หลัง action error และ stream resource cleanup. v8.5 deprecates Router-owned view transition API เพื่อใช้ React 19.3 `<ViewTransition>`. อ่าน [changelog](https://reactrouter.com/changelog), โดยเฉพาะ migration และ request cancellation.

## แนวคิดและคู่มือภายใน Vault

[[HTTP Request Lifecycle]] · [[HTTP Semantics and REST]] · [[React Server and Client Components]] · [[Technical-Knowledge/00-Home/Recent-Updates|สรุปอัปเดตทั้งหมด]]
