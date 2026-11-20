---
title: "Redis Persistence and Durability Choices"
type: concept
domain: redis
level: intermediate-to-advanced
tags: [redis, persistence, caching]
status: researched
last_verified: 2026-11-20
sources:
  - https://redis.io/docs/latest/operate/oss_and_stack/management/persistence/
---

# Redis Persistence and Durability Choices

## Overview

Redis มักถูกใช้เป็น cache แต่รองรับ persistence modes ที่ให้ durability/performance trade-offs ต่างกัน; การเลือกต้องระบุว่า data loss ยอมรับได้เท่าไร

## How it works

RDB snapshots เขียน dataset ณ จุดเวลา; AOF บันทึก write operations ตาม fsync policy; ใช้ร่วมกันได้ตาม version/config. Replication/cluster เพิ่ม availability/sharding แต่ไม่ได้แทน backup/restore. Cache key expiry/eviction เป็น lifecycle ของข้อมูลคนละเรื่องกับ disk persistence

## Example

```text
# inspect before deployment
CONFIG GET appendonly
CONFIG GET save
INFO persistence
INFO memory
```

ตัวอย่างเป็น pattern สั้น ๆ; ตรวจ API, dependencies และ runtime version กับ project ที่ใช้ก่อน deploy

## Common failure modes

เปิด persistence อย่างเดียวไม่ได้แปลว่ามี backup ที่กู้คืนผ่าน disaster; failover/replication อาจสูญ writes ล่าสุด; eviction policy ผิดทำให้ข้อมูลที่คิดว่า durable ถูกลบ

## Production practices

แยก cache dataset จาก source-of-truth, ทดสอบ restore ไป instance แยก, เลือก RDB/AOF ตาม RPO/latency, monitor disk/fsync/replication lag และทำ ACL/TLS

## Related knowledge

[[Redis]] · [[Redis Cache-Aside]] · [[Docker-Compose-Service-Networking-and-Health]] · [[Database-Transactions]]

## References

- [redis.io](https://redis.io/docs/latest/operate/oss_and_stack/management/persistence/)

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
