---
title: "Go Context"
type: concept
domain: go
level: intermediate
tags:
  - go
  - context
  - cancellation
status: researched
last_verified: 2026-11-20
sources:
  - https://pkg.go.dev/context
---

# Go Context

## Overview

context ส่ง deadline, cancellation และ request-scoped metadata ผ่าน call chain เพื่อให้การทำงานหยุดตามต้นทางได้

## กลไกและแนวคิดหลัก

สร้าง context ที่ boundary เช่น HTTP request แล้วส่งต่อไปยัง database/network calls; ลูกใช้ `ctx.Done()` หรือ API ที่รับ context เพื่อยกเลิกเมื่อ client disconnect, timeout หรือ parent cancel

## ตัวอย่าง

```go
ctx, cancel := context.WithTimeout(parent, 2*time.Second)
defer cancel()
row := db.QueryRowContext(ctx, query, id)
```

ตัวอย่างแสดงแนวคิดหลักเท่านั้น ให้เพิ่มการตรวจ input, resource cleanup และ error handling ตามบริบทก่อนใช้ production

## จุดพลาดและข้อควรระวัง

อย่าเก็บ context ไว้ใน struct ระยะยาว; อย่าส่ง nil; context value ใช้ metadata ที่ข้าม API boundary (เช่น trace ID) ไม่ใช่ optional function parameters ทุกชนิด และทุก `WithCancel/Timeout` ต้องเรียก cancel

## แนวทางใช้งาน

กำหนด timeout budget ต่อ request และแบ่งให้ dependency calls; ตรวจ cancellation ในงาน CPU loop เองเป็นระยะ

## ความสัมพันธ์

- Related: [[Go Goroutines]] · [[Go Channels]] · [[Gin]] · [[RabbitMQ]]
- เปิดภาพรวมหมวด: [[Technology-Index]] · [[Knowledge-Map]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://pkg.go.dev/context)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง
