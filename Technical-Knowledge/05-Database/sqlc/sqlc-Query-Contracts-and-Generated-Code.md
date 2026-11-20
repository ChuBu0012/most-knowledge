---
title: "sqlc Query Contracts and Generated Code"
type: concept
domain: sqlc
level: intermediate-to-advanced
tags: [sql, go, database, codegen]
status: researched
last_verified: 2026-11-20
sources:
  - https://docs.sqlc.dev/en/latest/howto/transactions.html
  - https://docs.sqlc.dev/en/latest/reference/config.html
---

# sqlc Query Contracts and Generated Code

## Overview

sqlc แปลง SQL ที่เขียนไว้เป็น typed methods; SQL ยังคงเป็น source of truth จึงตรวจ query plan และ database semantics ได้ตรง

## How it works

`.sql` files ใช้ annotations เช่น `:one`, `:many`, `:exec`; `sqlc.yaml` ระบุ engine/schema/queries และ generator. `sqlc generate` สร้าง code ที่รับ typed args/คืน typed rows. Database-backed analysis ช่วย infer complex queries ใน PostgreSQL ตาม feature status ปัจจุบัน

## Example

```sql
-- name: GetUser :one
SELECT id, email, created_at
FROM users
WHERE id = $1;

-- name: ListRecentUsers :many
SELECT id, email
FROM users
ORDER BY created_at DESC
LIMIT $1;
```

ตัวอย่างเป็น pattern สั้น ๆ; ตรวจ API, dependencies และ runtime version กับ project ที่ใช้ก่อน deploy

## Common failure modes

generated code compile ไม่ได้พิสูจน์ query performance; schema/query drift ทำให้ build stale ถ้าไม่ regenerate; SQL dialect differences และ nullable columns เปลี่ยน Go types

## Production practices

รัน generate และตรวจ diff ใน CI, ใช้ migrations เป็น schema source, จับ plan ด้วย `EXPLAIN`, parameterize all user input และควบคุม transaction จาก `Queries.WithTx`

## Related knowledge

[[sqlc]] · [[SQL]] · [[Database-Transactions]] · [[SQL Indexes and Query Plans]] · [[Go Testing]]

## References

- [docs.sqlc.dev](https://docs.sqlc.dev/en/latest/howto/transactions.html)
- [docs.sqlc.dev](https://docs.sqlc.dev/en/latest/reference/config.html)
