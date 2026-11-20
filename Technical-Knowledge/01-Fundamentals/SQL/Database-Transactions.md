---
title: "Database Transactions"
type: concept
domain: sql
level: intermediate
tags:
  - database
  - transactions
  - sql
status: researched
last_verified: 2026-11-20
sources:
  - https://www.postgresql.org/docs/current/tutorial-transactions.html
  - https://www.postgresql.org/docs/current/transaction-iso.html
---

# Database Transactions

## Overview

transaction ทำให้หลาย database operations เป็นหน่วยเดียวที่สำเร็จหรือย้อนกลับร่วมกัน

## กลไกและแนวคิดหลัก

ACID อธิบาย atomicity, consistency, isolation, durability. Transaction เปิด snapshot/locks ตาม engine และ isolation level; concurrent writes อาจทำให้เกิด lock waits, deadlocks หรือ serialization failures. ให้ transaction สั้นและ commit เมื่อ invariant ทางธุรกิจครบ

## ตัวอย่าง

```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 'A';
UPDATE accounts SET balance = balance + 100 WHERE id = 'B';
COMMIT;
```

ตัวอย่างแสดงแนวคิดหลักเท่านั้น ให้เพิ่มการตรวจ input, resource cleanup และ error handling ตามบริบทก่อนใช้ production

## จุดพลาดและข้อควรระวัง

ตัวอย่างต้องตรวจว่ามีบัญชีและยอดเงินถูกต้อง; transaction ที่มี network call ยาวเปิด lock นานและสร้างความเสี่ยง อย่าคิดว่า transaction ทำให้ distributed side effect เช่นส่ง email/queue ย้อนกลับได้ ใช้ outbox หรือ workflow เมื่อจำเป็น

## แนวทางใช้งาน

เมื่อ isolation level ทำให้ transaction abort ต้อง retry ทั้ง transaction อย่างปลอดภัย; ใช้ unique/foreign/check constraints เป็นแนวป้องกัน invariant ร่วมกับ application logic

## ความสัมพันธ์

- Related: [[SQL]] · [[PostgreSQL]] · [[Prisma]] · [[GORM]] · [[sqlc]] · [[RabbitMQ]]
- เปิดภาพรวมหมวด: [[Technology-Index]] · [[Knowledge-Map]]


## แหล่งอ้างอิง

- [PostgreSQL: Transactions](https://www.postgresql.org/docs/current/tutorial-transactions.html)
- [PostgreSQL: Transaction Isolation](https://www.postgresql.org/docs/current/transaction-iso.html)
