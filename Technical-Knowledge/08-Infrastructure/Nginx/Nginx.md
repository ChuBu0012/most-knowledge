---
title: "Nginx"
type: technology
domain: infrastructure
technology: "Nginx"
level: beginner-to-advanced
tags: [technical-knowledge, infrastructure, nginx]
status: overview
last_verified: 2026-11-20
sources:
  - https://nginx.org/en/docs/
  - https://nginx.org/en/CHANGES
---

# Nginx

## Overview

เว็บเซิร์ฟเวอร์และ reverse proxy รองรับ HTTP, TLS termination, load balancing และ static files

## เลือกใช้เมื่อ

รับ traffic หน้าแอป, serve assets หรือ route ไปหลาย backend

## ทำความเข้าใจให้ถูกก่อนเริ่ม

- หน้านี้เป็นแผนที่เริ่มต้น ไม่ใช่คู่มือ API ครบชุด ให้ยึดเอกสารทางการตามเวอร์ชันที่ติดตั้งจริง
- เวอร์ชันและความเข้ากันได้เปลี่ยนได้ ตรวจ release notes/compatibility ก่อนเริ่มโปรเจกต์หรืออัปเกรด
- เริ่มจากแนวคิดและตัวอย่างเล็ก แล้วค่อยนำไปผสานกับแอปจริง; อย่าคัดลอก config โดยไม่เข้าใจ runtime และ deployment target

## เส้นทางเรียนรู้

1. อ่าน Getting Started และเข้าใจ model หลักของเครื่องมือนี้
2. ทดลองตัวอย่างขั้นต่ำในโปรเจกต์แยก พร้อมบันทึก runtime, dependency และเวอร์ชัน
3. ศึกษาการจัดการ error, testing, security และ production configuration ที่เกี่ยวข้อง
4. เปรียบเทียบ trade-offs กับทางเลือกที่ลิงก์ด้านล่างก่อนยึดเป็นมาตรฐานของโปรเจกต์

## Update snapshot — 2026-11-20

As of 20 Nov 2026, nginx 1.30.7 is the stable line and 1.31.9 is mainline. Security fixes released in October affected alias/rewrite, variable expressions, HTTP/3 request bodies, TLS session tickets, and SSI with AIO; distributions may backport fixes, so check vendor advisories too.

แหล่งยืนยัน snapshot: - [https://nginx.org/en/download.html](https://nginx.org/en/download.html)
- [https://nginx.org/en/](https://nginx.org/en/)

## ความสัมพันธ์กับเรื่องอื่น

[[Docker]] · [[HTTP]] · [[FastAPI]]

## แหล่งข้อมูลและการตรวจสอบ

- [เอกสารทางการ](https://nginx.org/en/docs/)
- [ข่าว/รุ่น/มาตรฐาน](https://nginx.org/en/CHANGES)
- ตรวจลิงก์และสถานะเอกสารเมื่อ **2026-11-20**; หน้านี้ไม่ได้ pin patch version เพราะเอกสารต้นทางอัปเดตต่อเนื่อง

## อ่านเนื้อหาออฟไลน์

หัวข้อเหล่านี้อธิบายแนวคิดและการตัดสินใจที่เกี่ยวข้อง โดยเนื้อหาสำคัญอยู่ใน Vault ไม่ต้องเปิดเว็บเพื่ออ่านพื้นฐาน:

[[Nginx Reverse Proxy Request Flow]] · [[HTTP Request Lifecycle]] · [[Cookie and Session Security]]
