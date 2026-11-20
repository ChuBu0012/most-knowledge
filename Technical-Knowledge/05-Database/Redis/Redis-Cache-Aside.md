---
title: "Redis Cache-Aside"
type: concept
domain: redis
level: intermediate-to-advanced
tags: [redis, caching, database]
status: researched
last_verified: 2026-11-20
sources:
  - https://redis.io/docs/latest/develop/use/patterns/
---

# Redis Cache-Aside

## Overview

cache-aside ให้ application อ่าน cache ก่อน; เมื่อ miss จึงอ่าน primary database แล้วเติม cache พร้อม expiry

## กลไกและแนวคิดหลัก

cache key ต้องรวม input ที่กำหนดผลลัพธ์ เช่น tenant, locale, page และ authorization scope. TTL จำกัดเวลาค้างของ stale value แต่ไม่ได้รับประกัน consistency ทันที. เขียนข้อมูลหลักก่อน invalidate/update cache และจัดการ concurrent misses ตามต้นทุนระบบ

## ตัวอย่าง

```text
value = GET cache[key]
if value is miss:
    value = database.query(key)
    SET cache[key] value EX ttl
return value
```

ตัวอย่างเป็น schematic ที่สื่อหลักการ; ตรวจ syntax และ config ให้ตรงกับ version/runtime ที่ใช้งานก่อนนำไป deploy

## จุดพลาดและข้อควรระวัง

cache stampede ทำให้ miss พร้อมกันยิง database จำนวนมาก; cache poisoning/tenant key collision ทำให้ข้อมูลรั่ว; Redis eviction/outage ต้องมี fallback; อย่าถือ cache เป็น durable source of truth เว้นแต่ตั้ง durability/consistency ไว้ชัด

## แนวทางปฏิบัติ

กำหนด TTL และ memory policy, ทำ key namespacing/versioning, metrics hit/miss/eviction, timeout/fallback และทดสอบเมื่อ Redis หยุด

## ความสัมพันธ์

[[Redis]] · [[Database-Transactions]] · [[Prisma]] · [[GORM]] · [[sqlc]] · [[Docker-Compose]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://redis.io/docs/latest/develop/use/patterns/)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง
