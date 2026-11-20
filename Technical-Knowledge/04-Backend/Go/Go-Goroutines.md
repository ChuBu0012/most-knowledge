---
title: "Go Goroutines"
type: concept
domain: go
level: intermediate
tags:
  - go
  - concurrency
status: researched
last_verified: 2026-11-20
sources:
  - https://go.dev/tour/concurrency/1
---

# Go Goroutines

## Overview

goroutine คือหน่วย execution เบาที่ Go runtime จัดการ เหมาะกับงาน concurrent ที่ต้องรอ I/O หรือประมวลผลแยกกัน

## กลไกและแนวคิดหลัก

`go f()` เริ่ม goroutine แต่ไม่ได้สร้างการรับประกันว่า main รอผลหรือว่า shared state ปลอดภัย งานต้องมี lifecycle: ใครเริ่ม, ส่งผลอย่างไร, cancellation เมื่อไร และรอจบอย่างไร โดยใช้ channel, `sync.WaitGroup` หรือ `errgroup` ตาม use case

## ตัวอย่าง

```go
var wg sync.WaitGroup
for _, url := range urls {
    wg.Add(1)
    go func(url string) {
        defer wg.Done()
        fetch(url)
    }(url)
}
wg.Wait()
```

ตัวอย่างแสดงแนวคิดหลักเท่านั้น ให้เพิ่มการตรวจ input, resource cleanup และ error handling ตามบริบทก่อนใช้ production

## จุดพลาดและข้อควรระวัง

จำนวน goroutine ไม่จำกัดอาจทำให้ resource หมดและ shutdown ค้าง; loop capture variable ต้องเข้าใจ semantics ของ Go version ที่ใช้งาน; race detector ช่วยค้น data race แต่ไม่ได้พิสูจน์ absence of race

## แนวทางใช้งาน

จำกัด concurrency สำหรับงานจำนวนมาก, ส่ง context เข้า I/O, ใช้ synchronization ที่ชัดเจน และรัน `go test -race` ในงานที่เหมาะสม

## ความสัมพันธ์

- Related: [[Go Channels]] · [[Go Context]] · [[Go Testing]] · [[RabbitMQ]]
- เปิดภาพรวมหมวด: [[Technology-Index]] · [[Knowledge-Map]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://go.dev/tour/concurrency/1)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
