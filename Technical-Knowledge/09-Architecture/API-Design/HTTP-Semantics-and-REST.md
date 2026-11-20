---
title: "HTTP Semantics and REST"
type: concept
domain: http
level: intermediate
tags:
  - http
  - api-design
  - rest
status: researched
last_verified: 2026-11-20
sources:
  - https://www.rfc-editor.org/rfc/rfc9110
---

# HTTP Semantics and REST

## Overview

การออกแบบ HTTP API ใช้ semantics ของ method, status และ representation เพื่อให้ client/cache/proxy ทำงานร่วมกันได้

## กลไกและแนวคิดหลัก

GET ขอ representation และควร safe/idempotent; PUT แทน resource และ idempotent; POST สร้างหรือสั่งประมวลผลซึ่งอาจไม่ idempotent; DELETE idempotent ใน intended effect. Status 2xx success, 3xx redirect/cache, 4xx client/request issue, 5xx server/upstream issue. REST เป็นชุด constraints ด้าน resource, uniform interface และ statelessness ไม่ใช่แค่ใช้ JSON ผ่าน HTTP

## ตัวอย่าง

```javascript
POST /orders
Idempotency-Key: 6b7...
Content-Type: application/json

{"items":[{"sku":"A1","quantity":2}]}
```

ตัวอย่างแสดงแนวคิดหลักเท่านั้น ให้เพิ่มการตรวจ input, resource cleanup และ error handling ตามบริบทก่อนใช้ production

## จุดพลาดและข้อควรระวัง

ใช้ pagination/filtering ที่มีขอบเขต, validate input, รักษา backward compatibility และออกแบบ error response ให้มี machine-readable code. ถ้าคำสั่ง POST อาจถูก retry หลัง timeout ให้ใช้ idempotency key; อย่าใช้ GET เปลี่ยนข้อมูล

## แนวทางใช้งาน

เขียน OpenAPI contract ให้สอดคล้องกับ implementation และทดสอบ method/status, auth failure, validation และ pagination

## ความสัมพันธ์

- Related: [[HTTP Request Lifecycle]] · [[OpenAPI]] · [[OAuth-2.0]] · [[FastAPI]] · [[Gin]]
- เปิดภาพรวมหมวด: [[Technology-Index]] · [[Knowledge-Map]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://www.rfc-editor.org/rfc/rfc9110)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
