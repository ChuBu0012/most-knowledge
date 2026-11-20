---
title: "TanStack Query"
type: technology
domain: frontend-libraries
technology: "TanStack Query"
level: beginner-to-advanced
tags: [technical-knowledge, frontend-libraries, tanstack]
status: overview
last_verified: 2026-11-20
sources:
  - https://tanstack.com/query/latest/docs/framework/react/overview
  - https://tanstack.com/blog
---

# TanStack Query

## Overview

จัดการ server state: fetch, cache, synchronize, invalidate และ mutation ของข้อมูลจาก server

## เลือกใช้เมื่อ

ข้อมูล remote มี loading/error/cache/refetch lifecycle ที่ซับซ้อน

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

TanStack Query v5.108.1 packages were published 19 Nov; the release fixed infinite-query client methods to require `getNextPageParam`. The core model remains query-key identity, freshness, observers, retries, and invalidation; Svelte adapter versions can differ from the other framework adapters.

แหล่งยืนยัน snapshot: - [https://github.com/TanStack/query/releases](https://github.com/TanStack/query/releases)
- [https://tanstack.com/query/latest/docs/framework/react/overview](https://tanstack.com/query/latest/docs/framework/react/overview)

## ความสัมพันธ์กับเรื่องอื่น

[[React]] · [[Vue]] · [[Zod]] · [[TanStack Table]]

## แหล่งข้อมูลและการตรวจสอบ

- [เอกสารทางการ](https://tanstack.com/query/latest/docs/framework/react/overview)
- [ข่าว/รุ่น/มาตรฐาน](https://tanstack.com/blog)
- ตรวจลิงก์และสถานะเอกสารเมื่อ **2026-11-20**; หน้านี้ไม่ได้ pin patch version เพราะเอกสารต้นทางอัปเดตต่อเนื่อง

## อ่านเนื้อหาออฟไลน์

หัวข้อเหล่านี้อธิบายแนวคิดและการตัดสินใจที่เกี่ยวข้อง โดยเนื้อหาสำคัญอยู่ใน Vault ไม่ต้องเปิดเว็บเพื่ออ่านพื้นฐาน:

[[TanStack Query Cache Lifecycle]] · [[JavaScript Promises]] · [[Database-Transactions]]
