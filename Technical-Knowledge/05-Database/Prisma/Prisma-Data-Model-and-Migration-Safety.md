---
title: "Prisma Data Model and Migration Safety"
type: concept
domain: prisma
level: intermediate-to-advanced
tags: [prisma, database, migrations]
status: researched
last_verified: 2026-11-20
sources:
  - https://www.prisma.io/docs/orm/release-status
  - https://www.prisma.io/docs/guides/upgrade-prisma-orm
---

# Prisma Data Model and Migration Safety

## Overview

Prisma model/schema เป็น contract ระหว่าง application types กับ relational/document data; migration เปลี่ยน schema จริงและอาจทำลายข้อมูล

## How it works

Prisma ORM 7 ใช้ `schema.prisma` และ generated client workflow; Prisma 8 ยัง RC ณ 20 Nov 2026 เปลี่ยนไป contract model, query API และ migration process พร้อม database-specific packages ที่สถานะต่างกัน. Migration history ต้อง version-control และประเมิน generated SQL ก่อน apply

## Example

```bash
// Migration workflow (Prisma ORM 7 pattern)
npx prisma migrate dev --name add-status
npx prisma migrate deploy
// review generated SQL and back up data before production rollout
```

ตัวอย่างเป็น pattern สั้น ๆ; ตรวจ API, dependencies และ runtime version กับ project ที่ใช้ก่อน deploy

## Common failure modes

อย่าใช้ dev migration command ใน production; schema push แบบไม่เก็บ migration history ลด auditability; destructive rename/drop ต้องตรวจ data retention; Prisma 8 RC มี feature gaps/connectors ที่ยัง preview

## Production practices

แยก expand/contract migration สำหรับ rolling deploy, test migration บน copy/staging, backup/restore drill และ pin `prisma` + client packages ตาม major/status

## Related knowledge

[[Prisma]] · [[Database-Transactions]] · [[SQL Indexes and Query Plans]] · [[Database Connection Pooling]]

## References

- [www.prisma.io](https://www.prisma.io/docs/orm/release-status)
- [www.prisma.io](https://www.prisma.io/docs/guides/upgrade-prisma-orm)
