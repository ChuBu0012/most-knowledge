---
title: "Prisma"
type: technology
domain: database
technology: "Prisma"
level: beginner-to-advanced
tags: [technical-knowledge, database, prisma]
status: overview
last_verified: 2026-11-20
sources:
  - https://www.prisma.io/docs
  - https://www.prisma.io/changelog
  - https://www.prisma.io/docs/orm/release-status
---

# Prisma

## Overview

ORM/toolkit สำหรับ TypeScript/Node.js ให้ schema, client ที่สร้างอัตโนมัติ และ migrations

## เลือกใช้เมื่อ

แอป TS ต้องการ data model และ query API ที่ type-safe

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

[[TypeScript]] · [[Database Transactions]] · [[PostgreSQL]]

## แหล่งข้อมูลและการตรวจสอบ

- [เอกสารทางการ](https://www.prisma.io/docs)
- [ข่าว/รุ่น/มาตรฐาน](https://www.prisma.io/changelog)
- ตรวจลิงก์และสถานะเอกสารเมื่อ **2026-11-20**; หน้านี้ไม่ได้ pin patch version เพราะเอกสารต้นทางอัปเดตต่อเนื่อง

## อ่านเนื้อหาออฟไลน์

หัวข้อเหล่านี้อธิบายแนวคิดและการตัดสินใจที่เกี่ยวข้อง โดยเนื้อหาสำคัญอยู่ใน Vault ไม่ต้องเปิดเว็บเพื่ออ่านพื้นฐาน:

[[Database-Transactions]] · [[SQL Indexes and Query Plans]] · [[Database Connection Pooling]]

## Update snapshot — 2026-11-20

Prisma ORM 8 ยังเป็น release candidate ณ 20 Nov 2026; อย่าเข้าใจว่าเป็น GA แม้ package tag `latest` ชี้ไป RC. CLI และ database adapter libraries version แยกกัน; บาง connector ยัง early access/experimental. Prisma 7 มี docs/major track ของตัวเอง.

## แนวคิดและคู่มือภายใน Vault

[[Database-Transactions]] · [[SQL Indexes and Query Plans]] · [[Database Connection Pooling]] · [[Technical-Knowledge/00-Home/Recent-Updates|สรุปอัปเดตทั้งหมด]]


## คำสั่งและสูตรใช้งาน

[[Technical-Knowledge/12-Command-Reference/Prisma/Prisma-Recipes|Prisma Recipes]] — ตัวอย่าง API/คำสั่งที่ใช้บ่อย

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
