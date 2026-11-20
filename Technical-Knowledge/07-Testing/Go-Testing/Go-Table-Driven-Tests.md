---
title: "Go Table-Driven Tests"
type: concept
domain: go
level: intermediate-to-advanced
tags: [go, testing]
status: researched
last_verified: 2026-11-20
sources:
  - https://go.dev/doc/tutorial/add-a-test
---

# Go Table-Driven Tests

## Overview

table-driven test ใช้ cases ที่ระบุ input, expected output และชื่อกรณี เพื่อทดสอบ behavior หลายขอบเขตด้วยโครงสร้างเดียว

## กลไกและแนวคิดหลัก

Go test discovery รัน `TestXxx(*testing.T)`; subtests ผ่าน `t.Run` ให้แยกผล/รันเจาะกรณี. ใช้ `t.Parallel` เฉพาะเมื่อ test ไม่มี shared mutable state และ test data/config แยกกัน. Fuzz tests สำรวจ input ที่หลากหลาย; benchmarks วัดงานซ้ำในเงื่อนไขควบคุม

## ตัวอย่าง

```go
tests := []struct {
  name string
  input int
  want bool
}{
  {"zero", 0, false},
  {"positive", 3, true},
}
for _, tt := range tests {
  t.Run(tt.name, func(t *testing.T) { /* assert */ })
}
```

ตัวอย่างเป็น schematic ที่สื่อหลักการ; ตรวจ syntax และ config ให้ตรงกับ version/runtime ที่ใช้งานก่อนนำไป deploy

## จุดพลาดและข้อควรระวัง

assertion helper ที่ซ่อน context ทำให้ failure อ่านยาก; parallel test ที่เปลี่ยน global env/timezone มี race; benchmark ผลไม่เท่ากับ production profile

## แนวทางปฏิบัติ

ทดสอบ public behavior, ใช้ deterministic clock/dependencies, รัน race detector กับ concurrency และ fuzz parser/boundary inputs ที่เสี่ยง

## ความสัมพันธ์

[[Go Testing]] · [[Go Error Handling]] · [[Unit Integration and End-to-End Tests]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://go.dev/doc/tutorial/add-a-test)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
