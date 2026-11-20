---
title: "Fiber"
type: technology
domain: backend
technology: "Fiber"
level: beginner-to-advanced
tags: [technical-knowledge, backend, fiber]
status: overview
last_verified: 2026-11-20
sources:
  - https://docs.gofiber.io/
  - https://github.com/gofiber/fiber/releases
---

# Fiber

## Overview

Go web framework ที่มี API คล้าย Express และสร้างบน fasthttp พร้อม middleware ecosystem

## เลือกใช้เมื่อ

ทีมที่คุ้น Express หรือมีเหตุผลด้าน performance/runtime ให้เลือก fasthttp

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

[[Go]] · [[Gin]] · [[Express]]

## แหล่งข้อมูลและการตรวจสอบ

- [เอกสารทางการ](https://docs.gofiber.io/)
- [ข่าว/รุ่น/มาตรฐาน](https://github.com/gofiber/fiber/releases)
- ตรวจลิงก์และสถานะเอกสารเมื่อ **2026-11-20**; หน้านี้ไม่ได้ pin patch version เพราะเอกสารต้นทางอัปเดตต่อเนื่อง

## อ่านเนื้อหาออฟไลน์

หัวข้อเหล่านี้อธิบายแนวคิดและการตัดสินใจที่เกี่ยวข้อง โดยเนื้อหาสำคัญอยู่ใน Vault ไม่ต้องเปิดเว็บเพื่ออ่านพื้นฐาน:

[[HTTP Request Lifecycle]] · [[HTTP Semantics and REST]] · [[Go Context]]

## Update snapshot — 2026-11-20

Fiber v3.7.0 (9 Nov 2026) อัปเดต fasthttp 1.78 และรองรับ map fields ใน query/form binder; Fiber v3.6 กำหนด Go 1.26+. Fiber ใช้ fasthttp APIs ซึ่งไม่เท่ากับ `net/http`.

## แนวคิดและคู่มือภายใน Vault

[[HTTP Request Lifecycle]] · [[HTTP Semantics and REST]] · [[Go Context]] · [[Technical-Knowledge/00-Home/Recent-Updates|สรุปอัปเดตทั้งหมด]]


## คำสั่งและสูตรใช้งาน

[[Fiber Recipes]] — เริ่มต้น, routes/handlers, validation, errors และการรัน

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
