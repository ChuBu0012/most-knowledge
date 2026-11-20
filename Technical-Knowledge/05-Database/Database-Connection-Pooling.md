---
title: "Database Connection Pooling"
type: concept
domain: sql
level: intermediate-to-advanced
tags: [database, connections, pooling]
status: researched
last_verified: 2026-11-20
sources:
  - https://www.postgresql.org/docs/current/runtime-config-connection.html
---

# Database Connection Pooling

## Overview

connection pool reuse database connections เพื่อเลี่ยง handshake/auth overhead และจำกัดจำนวน session ที่ backend เปิดพร้อมกัน

## กลไกและแนวคิดหลัก

แต่ละ pool มี max open, idle, lifetime และ wait queue. จำนวน connection รวมจากทุก process/replica อาจเกิน database limit แม้แต่ละ service ดูเหมือนตั้งค่าต่ำ. Query ใช้ connection จน transaction/rows ปิด; leak ทำให้ pool exhausted และ latency เพิ่ม

## ตัวอย่าง

```typescript
// Go database/sql
 db.SetMaxOpenConns(20)
 db.SetMaxIdleConns(10)
 db.SetConnMaxLifetime(30 * time.Minute)
```

ตัวอย่างเป็น schematic ที่สื่อหลักการ; ตรวจ syntax และ config ให้ตรงกับ version/runtime ที่ใช้งานก่อนนำไป deploy

## จุดพลาดและข้อควรระวัง

อย่าตั้ง pool ให้เท่ากับจำนวน request concurrency โดยอัตโนมัติ; transaction ยาวผูก connection; serverless scale-out อาจสร้าง connection storm. ตรวจ pool wait time และ query time แยกกัน

## แนวทางปฏิบัติ

กำหนด connection budget รวมทั้ง fleet, ปิด rows/transactions เสมอ, ตั้ง timeout ผ่าน context และใช้ proxy/pooler ตาม database architecture

## ความสัมพันธ์

[[Database-Transactions]] · [[SQL Indexes and Query Plans]] · [[Prisma]] · [[GORM]] · [[sqlc]] · [[PostgreSQL]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://www.postgresql.org/docs/current/runtime-config-connection.html)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง
