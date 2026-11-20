---
title: "Go Error Handling"
type: concept
domain: go
level: intermediate
tags:
  - go
  - errors
status: researched
last_verified: 2026-11-20
sources:
  - https://go.dev/blog/error-handling-and-go
---

# Go Error Handling

## Overview

Go ใช้ error เป็นค่าที่ส่งกลับอย่างชัดแจ้ง ทำให้เส้นทาง failure ปรากฏใน control flow

## กลไกและแนวคิดหลัก

ฟังก์ชันมักคืน `(value, error)`; caller ตรวจ `err != nil`. เพิ่มบริบทด้วย `%w` เพื่อให้ `errors.Is`/`errors.As` ตรวจต้นเหตุหรือชนิดได้ โดยแยก error ที่ใช้ตัดสินใจออกจากข้อความสำหรับ log

## ตัวอย่าง

```go
f, err := os.Open(path)
if err != nil {
    return fmt.Errorf("open config %q: %w", path, err)
}
defer f.Close()
```

ตัวอย่างแสดงแนวคิดหลักเท่านั้น ให้เพิ่มการตรวจ input, resource cleanup และ error handling ตามบริบทก่อนใช้ production

## จุดพลาดและข้อควรระวัง

อย่า log แล้วคืน error เดิมทุกชั้นจน log ซ้ำ; อย่าเปรียบเทียบข้อความ error; อย่าทิ้ง error ของ Close/transaction cleanup โดยไม่พิจารณา ใช้ sentinel error เมื่อ caller ต้องแยกกรณีเชิงตรรกะ

## แนวทางใช้งาน

เพิ่ม context ที่ชั้น abstraction เปลี่ยน error ให้เป็น HTTP status ที่ boundary และไม่เปิดเผย internals ต่อ client

## ความสัมพันธ์

- Related: [[Go]] · [[Gin]] · [[Fiber]] · [[Go Testing]]
- เปิดภาพรวมหมวด: [[Technology-Index]] · [[Knowledge-Map]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://go.dev/blog/error-handling-and-go)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง
