---
title: "Go Channels"
type: concept
domain: go
level: intermediate
tags:
  - go
  - concurrency
  - channels
status: researched
last_verified: 2026-11-20
sources:
  - https://go.dev/tour/concurrency/2
---

# Go Channels

## Overview

channel เป็น typed conduit สำหรับส่งค่าและประสานงานระหว่าง goroutines

## กลไกและแนวคิดหลัก

unbuffered channel ทำให้ sender/receiver rendezvous; buffered channel อนุญาตให้ส่งได้ถึง capacity ก่อน block. `close` บอกว่าไม่มีค่าจะส่งอีก ผู้ส่งเป็นเจ้าของการ close โดยทั่วไป receiver ใช้ `range` เพื่ออ่านจน channel ปิด

## ตัวอย่าง

```go
jobs := make(chan Job)
go func() {
    defer close(jobs)
    for _, job := range input { jobs <- job }
}()
for job := range jobs { process(job) }
```

ตัวอย่างแสดงแนวคิดหลักเท่านั้น ให้เพิ่มการตรวจ input, resource cleanup และ error handling ตามบริบทก่อนใช้ production

## จุดพลาดและข้อควรระวัง

ส่งไปยัง channel ที่ไม่มี receiver อาจค้าง; ปิด channel ซ้ำหรือส่งหลังปิดจะ panic; ไม่จำเป็นต้องใช้ channel แทน mutex สำหรับทุก shared state และ channel ที่ไม่มี owner ชัดทำให้ shutdown ยาก

## แนวทางใช้งาน

ใช้ channel เมื่อสื่อสาร/ส่ง ownership; ใช้ mutex เมื่อปกป้อง state ที่แชร์ ใช้ `select` ร่วมกับ context เพื่อให้รอหลายเหตุการณ์และ cancellation ได้

## ความสัมพันธ์

- Related: [[Go Goroutines]] · [[Go Context]] · [[Go Testing]]
- เปิดภาพรวมหมวด: [[Technology-Index]] · [[Knowledge-Map]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://go.dev/tour/concurrency/2)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
