---
title: "GORM Transactions and Associations"
type: concept
domain: gorm
level: intermediate-to-advanced
tags: [gorm, go, database]
status: researched
last_verified: 2026-11-20
sources:
  - https://gorm.io/docs/transactions.html
  - https://gorm.io/docs/preload.html
---

# GORM Transactions and Associations

## Overview

GORM map struct models ไป table/associations และให้ CRUD API; transaction boundary ควรตาม invariant ทางธุรกิจ ไม่ใช่จำนวน method calls

## How it works

GORM `Transaction` ให้ callback ที่ commit เมื่อคืน nil และ rollback เมื่อคืน error. Associations/Preload ทำ eager loading แต่ join count/query shape มีผลกับ performance. GORM conventions (primary key, table naming, timestamps) เปลี่ยน SQL ที่สร้าง จึงควรรู้ naming strategy

## Example

```go
err := db.Transaction(func(tx *gorm.DB) error {
  if err := tx.Create(&order).Error; err != nil { return err }
  return tx.Model(&account).Update("balance", nextBalance).Error
})
```

ตัวอย่างเป็น pattern สั้น ๆ; ตรวจ API, dependencies และ runtime version กับ project ที่ใช้ก่อน deploy

## Common failure modes

ใช้ `db` แทน `tx` ภายใน transaction ทำให้ query หลุด atomic boundary; Preload หลาย associations สร้าง query/ข้อมูลมาก; AutoMigrate ไม่แทน schema migration review ใน production

## Production practices

ตรวจ generated SQL/logs, ใช้ explicit constraints/indexes, จำกัด Preload, return errors ทุก operation และทดสอบ rollback เมื่อ operation กลางทางล้มเหลว

## Related knowledge

[[GORM]] · [[Database-Transactions]] · [[SQL Indexes and Query Plans]] · [[Database Connection Pooling]] · [[Go Error Handling]]

## References

- [gorm.io](https://gorm.io/docs/transactions.html)
- [gorm.io](https://gorm.io/docs/preload.html)
