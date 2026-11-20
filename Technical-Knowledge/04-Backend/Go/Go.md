---
title: "Go"
type: technology
domain: backend
technology: "Go"
level: beginner-to-advanced
tags: [technical-knowledge, backend, go]
status: overview
last_verified: 2026-11-20
sources:
  - https://go.dev/doc/
  - https://go.dev/doc/devel/release
  - https://go.dev/doc/go1.27
---

# Go

## Overview

ภาษา compiled ที่เน้นความเรียบง่าย, concurrency ผ่าน goroutine/channel และเครื่องมือมาตรฐานสำหรับ service

## เลือกใช้เมื่อ

บริการ backend, CLI และระบบที่ต้องการ deploy เป็น binary เดียว

## ทำความเข้าใจให้ถูกก่อนเริ่ม

- หน้านี้เป็นแผนที่เริ่มต้น ไม่ใช่คู่มือ API ครบชุด ให้ยึดเอกสารทางการตามเวอร์ชันที่ติดตั้งจริง
- เวอร์ชันและความเข้ากันได้เปลี่ยนได้ ตรวจ release notes/compatibility ก่อนเริ่มโปรเจกต์หรืออัปเกรด
- เริ่มจากแนวคิดและตัวอย่างเล็ก แล้วค่อยนำไปผสานกับแอปจริง; อย่าคัดลอก config โดยไม่เข้าใจ runtime และ deployment target

## เส้นทางเรียนรู้

1. อ่าน Getting Started และเข้าใจ model หลักของเครื่องมือนี้
2. ทดลองตัวอย่างขั้นต่ำในโปรเจกต์แยก พร้อมบันทึก runtime, dependency และเวอร์ชัน
3. ศึกษาการจัดการ error, testing, security และ production configuration ที่เกี่ยวข้อง
4. เปรียบเทียบ trade-offs กับทางเลือกที่ลิงก์ด้านล่างก่อนยึดเป็นมาตรฐานของโปรเจกต์

## ความสัมพันธ์กับเรื่องอื่น

[[Gin]] · [[Fiber]] · [[Go Testing]] · [[sqlc]]

## แหล่งข้อมูลและการตรวจสอบ

- [เอกสารทางการ](https://go.dev/doc/)
- [ข่าว/รุ่น/มาตรฐาน](https://go.dev/doc/devel/release)
- ตรวจลิงก์และสถานะเอกสารเมื่อ **2026-11-20**; หน้านี้ไม่ได้ pin patch version เพราะเอกสารต้นทางอัปเดตต่อเนื่อง

## อ่านเนื้อหาออฟไลน์

หัวข้อเหล่านี้อธิบายแนวคิดและการตัดสินใจที่เกี่ยวข้อง โดยเนื้อหาสำคัญอยู่ใน Vault ไม่ต้องเปิดเว็บเพื่ออ่านพื้นฐาน:

[[Go Error Handling]] · [[Go Goroutines]] · [[Go Channels]] · [[Go Context]]

## Update snapshot — 2026-11-20

Go 1.27.4 (10 Nov 2026) เป็น patch ล่าสุดที่ตรวจ; 1.27 เพิ่ม generic methods, `encoding/json/v2`/`jsontext`, UUID package และการปรับ TLS. `go.mod` version และ toolchain floor มีผลต่อ syntax/runtime ที่ใช้.

## แนวคิดและคู่มือภายใน Vault

[[Go Error Handling]] · [[Go Goroutines]] · [[Go Channels]] · [[Go Context]] · [[Technical-Knowledge/00-Home/Recent-Updates|สรุปอัปเดตทั้งหมด]]


## คำสั่งและสูตรใช้งาน

[[Go Recipes]] — ค้น API/คำสั่งจากงานที่ต้องทำ พร้อมตัวอย่างและข้อควรระวัง

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
