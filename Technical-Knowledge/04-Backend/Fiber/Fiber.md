---
title: "Fiber"
type: technology
domain: fiber
technology: "Fiber"
level: beginner-to-advanced
tags:
  - fiber
  - fiber
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
