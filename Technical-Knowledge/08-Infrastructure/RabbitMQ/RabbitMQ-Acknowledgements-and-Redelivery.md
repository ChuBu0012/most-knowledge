---
title: "RabbitMQ Acknowledgements and Redelivery"
type: concept
domain: rabbitmq
level: intermediate-to-advanced
tags: [rabbitmq, messaging, reliability]
status: researched
last_verified: 2026-11-20
sources:
  - https://www.rabbitmq.com/docs/confirms
---

# RabbitMQ Acknowledgements and Redelivery

## Overview

broker delivery เป็น asynchronous handoff; publisher confirm และ consumer acknowledgement เป็นคนละทิศทางและคนละหลักประกัน

## กลไกและแนวคิดหลัก

publisher confirm บอก broker ว่ารับ publish แล้ว; consumer ack บอก broker ว่า consumer จัดการ delivery เสร็จ. หาก consumer crash ก่อน ack message อาจถูก redeliver. ดังนั้น consumer ควร idempotent หรือใช้ deduplication key. Durable queue/message และ quorum queue มี trade-offs ด้าน availability/latency

## ตัวอย่าง

```typescript
// pseudocode
process(message)
ack(message)        // หลัง side effect สำเร็จ
// เมื่อ retry ไม่เหมาะ: reject/nack แล้ว route ไป DLQ ตาม policy
```

ตัวอย่างเป็น schematic ที่สื่อหลักการ; ตรวจ syntax และ config ให้ตรงกับ version/runtime ที่ใช้งานก่อนนำไป deploy

## จุดพลาดและข้อควรระวัง

auto-ack เสี่ยง message หายเมื่อ process ล้ม; ack ก่อน commit database สร้าง inconsistency; requeue วนไม่จำกัดทำ poison-message loop; “exactly once” end-to-end ไม่ได้มาฟรีจาก broker

## แนวทางปฏิบัติ

กำหนด retry/backoff และ dead-letter policy, จำกัด prefetch, ใช้ idempotent handler/outbox, monitor queue depth/consumer lag และตรวจ publisher confirms

## ความสัมพันธ์

[[RabbitMQ]] · [[Database-Transactions]] · [[Go Context]] · [[Docker-Compose-Service-Networking-and-Health]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://www.rabbitmq.com/docs/confirms)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
