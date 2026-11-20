---
title: "sqlc"
type: technology
domain: database
technology: "sqlc"
level: beginner-to-advanced
tags: [technical-knowledge, database, sqlc]
status: overview
last_verified: 2026-11-20
sources:
  - https://docs.sqlc.dev/en/latest/
  - https://github.com/sqlc-dev/sqlc/releases
---

# sqlc

## Overview

สร้างโค้ด Go/ภาษาอื่นจาก SQL ที่เขียนเอง ให้ query ตรวจได้และผลลัพธ์มีชนิดข้อมูล

## เลือกใช้เมื่อ

ต้องการควบคุม SQL และได้ type-safe database layer

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

sqlc v1.31.1 is the current release line observed. The core workflow remains SQL-first: declare schema and queries, generate typed code, then review generated query behavior and database-specific support before upgrading.

แหล่งยืนยัน snapshot: - [https://github.com/sqlc-dev/sqlc/releases](https://github.com/sqlc-dev/sqlc/releases)
- [https://docs.sqlc.dev/en/latest/](https://docs.sqlc.dev/en/latest/)

## ความสัมพันธ์กับเรื่องอื่น

[[Go]] · [[SQL]] · [[Database Transactions]]

## แหล่งข้อมูลและการตรวจสอบ

- [เอกสารทางการ](https://docs.sqlc.dev/en/latest/)
- [ข่าว/รุ่น/มาตรฐาน](https://github.com/sqlc-dev/sqlc/releases)
- ตรวจลิงก์และสถานะเอกสารเมื่อ **2026-11-20**; หน้านี้ไม่ได้ pin patch version เพราะเอกสารต้นทางอัปเดตต่อเนื่อง

## อ่านเนื้อหาออฟไลน์

หัวข้อเหล่านี้อธิบายแนวคิดและการตัดสินใจที่เกี่ยวข้อง โดยเนื้อหาสำคัญอยู่ใน Vault ไม่ต้องเปิดเว็บเพื่ออ่านพื้นฐาน:

[[Database-Transactions]] · [[SQL Indexes and Query Plans]] · [[Database Connection Pooling]]


## คำสั่งและสูตรใช้งาน

[[Technical-Knowledge/12-Command-Reference/sqlc/sqlc-Recipes|sqlc Recipes]] — ตัวอย่าง API/คำสั่งที่ใช้บ่อย

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
