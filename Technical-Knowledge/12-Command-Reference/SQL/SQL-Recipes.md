---
title: SQL Recipes
type: reference
domain: sql
tags: [technical-knowledge, sql, api-reference, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://www.postgresql.org/docs/current/tutorial.html
  - https://www.postgresql.org/docs/current/sql.html
---

# SQL Recipes

ตัวอย่างใช้ PostgreSQL syntax เป็นหลัก; ความต่างระหว่าง PostgreSQL/MySQL/SQLite/SQL Server มีได้ โดยเฉพาะ upsert, returning, JSON และ pagination

## สร้าง table พร้อม constraint

```sql
CREATE TABLE users (
  id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
  email text NOT NULL UNIQUE,
  display_name text NOT NULL,
  created_at timestamptz NOT NULL DEFAULT now()
);
```

ใช้ `NOT NULL`, `UNIQUE`, foreign key และ `CHECK` เพื่อบังคับ invariant ในฐานข้อมูล ไม่ฝากความถูกต้องไว้กับ UI อย่างเดียว.

## อ่าน/กรอง/เรียงข้อมูล

```sql
SELECT id, email, created_at
FROM users
WHERE created_at >= $1
ORDER BY created_at DESC, id DESC
LIMIT $2;
```

เลือกเฉพาะ column ที่ต้องใช้; ใช้ parameter binding (`$1`) แทนต่อ string เพื่อป้องกัน SQL injection. เพิ่ม secondary sort key ให้ pagination มีลำดับแน่นอน.

## join ตาราง

```sql
SELECT o.id, o.created_at, u.email
FROM orders AS o
JOIN users AS u ON u.id = o.user_id
WHERE o.user_id = $1
ORDER BY o.created_at DESC;
```

กำหนด join key ชัด; ตรวจจำนวนแถวและ query plan. `LEFT JOIN` ใช้เมื่อแถวฝั่งซ้ายต้องอยู่แม้ไม่มีข้อมูลที่ match.

## เพิ่มข้อมูลและคืน row

```sql
INSERT INTO users (email, display_name)
VALUES ($1, $2)
RETURNING id, email, created_at;
```

`RETURNING` เป็น PostgreSQL feature; ORM/driver ต้อง bind parameters และอ่าน result ตาม protocol.

## Upsert ด้วย unique key

```sql
INSERT INTO users (email, display_name)
VALUES ($1, $2)
ON CONFLICT (email)
DO UPDATE SET display_name = EXCLUDED.display_name
RETURNING id;
```

ระบุ conflict target ที่มี constraint รองรับ. ระวัง upsert ที่ update ทุกครั้งอาจ trigger side effects, audit timestamps หรือ row locks.

## เปลี่ยนข้อมูลเป็น transaction

```sql
BEGIN;
UPDATE accounts SET balance = balance - $1 WHERE id = $2 AND balance >= $1;
-- ตรวจ row count ว่าหักสำเร็จ
UPDATE accounts SET balance = balance + $1 WHERE id = $3;
COMMIT;
```

ตรวจ row count และเงื่อนไขทางธุรกิจก่อน commit; เมื่อเกิด error ต้อง rollback. Transaction ไม่ครอบคลุม email/HTTP/queue side effects โดยอัตโนมัติ.

## ใช้ CTE แบ่ง query

```sql
WITH recent_orders AS (
  SELECT user_id, sum(total) AS spent
  FROM orders
  WHERE created_at >= $1
  GROUP BY user_id
)
SELECT u.id, u.email, r.spent
FROM recent_orders AS r
JOIN users AS u ON u.id = r.user_id
ORDER BY r.spent DESC;
```

CTE ตั้งชื่อขั้นตอนให้ query อ่านง่าย; ตรวจ execution plan เพราะ optimizer behavior ขึ้นกับ database/version และรูปแบบ query.

## ตรวจ index และ plan

```sql
CREATE INDEX orders_user_created_idx ON orders (user_id, created_at DESC);
EXPLAIN (ANALYZE, BUFFERS) SELECT ...;
```

`EXPLAIN ANALYZE` รัน query จริงและมีผลข้างเคียงหากเป็น write. Index ช่วยบาง access pattern แต่เพิ่มพื้นที่และต้นทุน insert/update; ดู selectivity, sort, cardinality และ production-like data.

## ค้นต่อ

[[SQL]] · [[Database Transactions]] · [[SQL Indexes and Query Plans]] · [[sqlc Query Contracts and Generated Code]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
