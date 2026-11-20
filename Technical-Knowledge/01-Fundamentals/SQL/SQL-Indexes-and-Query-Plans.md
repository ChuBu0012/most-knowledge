---
title: "SQL Indexes and Query Plans"
type: concept
domain: sql
level: intermediate
tags:
  - database
  - performance
  - indexes
status: researched
last_verified: 2026-11-20
sources:
  - https://www.postgresql.org/docs/current/using-explain.html
---

# SQL Indexes and Query Plans

## Overview

index เป็นโครงสร้างค้นหาที่แลกพื้นที่และค่าใช้จ่ายตอนเขียนเพื่อเร่ง query บางรูปแบบ

## กลไกและแนวคิดหลัก

B-tree เหมาะกับ equality/range และการเรียง; composite index ใช้ลำดับคอลัมน์มีผล; selectivity และ query predicate กำหนดว่าตัว planner เลือกใช้หรือไม่. `EXPLAIN` แสดงแผนโดยประมาณ; `EXPLAIN ANALYZE` รัน query จริง จึงมีผลข้างเคียงสำหรับ statement ที่เปลี่ยนข้อมูล

## ตัวอย่าง

```sql
CREATE INDEX orders_customer_created_idx
ON orders (customer_id, created_at DESC);

EXPLAIN ANALYZE
SELECT id, created_at FROM orders
WHERE customer_id = $1
ORDER BY created_at DESC LIMIT 20;
```

ตัวอย่างแสดงแนวคิดหลักเท่านั้น ให้เพิ่มการตรวจ input, resource cleanup และ error handling ตามบริบทก่อนใช้ production

## จุดพลาดและข้อควรระวัง

index ทุกอันกิน storage และเพิ่ม write amplification; function/cast บน indexed column อาจทำให้ใช้ index ไม่ได้; อย่าสรุปจากข้อมูลจำลองเล็ก ๆ เทียบแผนกับ production-like cardinality และ bind parameters

## แนวทางใช้งาน

วัดก่อน/หลังด้วย query plans และ latency metrics; ใช้ composite index ตาม filter/order จริง ไม่สร้าง index ซ้ำจากความรู้สึก

## ความสัมพันธ์

- Related: [[SQL]] · [[Database-Transactions]] · [[PostgreSQL]] · [[Prisma]] · [[sqlc]]
- เปิดภาพรวมหมวด: [[Technology-Index]] · [[Knowledge-Map]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://www.postgresql.org/docs/current/using-explain.html)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
