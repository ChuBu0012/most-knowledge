---
title: "GORM"
type: technology
domain: database
technology: "GORM"
level: beginner-to-advanced
tags: [technical-knowledge, database, gorm]
status: overview
last_verified: 2026-11-20
sources:
  - https://gorm.io/docs/
  - https://github.com/go-gorm/gorm/releases
---

# GORM

## Overview

ORM สำหรับ Go รองรับ model mapping, associations, callbacks และ migrations เบื้องต้น

## เลือกใช้เมื่อ

ต้องการพัฒนา CRUD ใน Go ด้วย abstraction ระดับ model

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

GORM v1.31.2 is the latest release observed; its fixes include cleanup behavior when a row iteration panics. Keep transaction boundaries explicit, close rows, and inspect generated SQL for performance-sensitive queries.

แหล่งยืนยัน snapshot: - [https://github.com/go-gorm/gorm/releases](https://github.com/go-gorm/gorm/releases)
- [https://gorm.io/docs/](https://gorm.io/docs/)

## ความสัมพันธ์กับเรื่องอื่น

[[Go]] · [[Database Transactions]] · [[sqlc]]

## แหล่งข้อมูลและการตรวจสอบ

- [เอกสารทางการ](https://gorm.io/docs/)
- [ข่าว/รุ่น/มาตรฐาน](https://github.com/go-gorm/gorm/releases)
- ตรวจลิงก์และสถานะเอกสารเมื่อ **2026-11-20**; หน้านี้ไม่ได้ pin patch version เพราะเอกสารต้นทางอัปเดตต่อเนื่อง

## อ่านเนื้อหาออฟไลน์

หัวข้อเหล่านี้อธิบายแนวคิดและการตัดสินใจที่เกี่ยวข้อง โดยเนื้อหาสำคัญอยู่ใน Vault ไม่ต้องเปิดเว็บเพื่ออ่านพื้นฐาน:

[[Go Error Handling]] · [[Database-Transactions]] · [[Database Connection Pooling]]


## คำสั่งและสูตรใช้งาน

[[Technical-Knowledge/12-Command-Reference/GORM/GORM-Recipes|GORM Recipes]] — ตัวอย่าง API/คำสั่งที่ใช้บ่อย

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
