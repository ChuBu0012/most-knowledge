---
title: "OAuth 2.0"
type: technology
domain: security
technology: "OAuth 2.0"
level: beginner-to-advanced
tags: [technical-knowledge, security, oauth-2.0]
status: overview
last_verified: 2026-11-20
sources:
  - https://www.rfc-editor.org/rfc/rfc6749
  - https://www.rfc-editor.org/rfc/rfc9700
---

# OAuth 2.0

## Overview

กรอบ authorization ให้ client เข้าถึงทรัพยากรด้วยสิทธิ์ที่ได้รับ โดยแยก resource owner, client และ authorization server

## เลือกใช้เมื่อ

ให้แอปเข้าถึง API ในนามผู้ใช้หรือเชื่อม identity provider

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

RFC 9700 remains the current OAuth 2.0 Security Best Current Practice. Prefer Authorization Code with PKCE, exact redirect URI matching, issuer-aware validation, and modern sender/client protections; avoid implicit and resource-owner-password flows.

แหล่งยืนยัน snapshot: - [https://www.rfc-editor.org/rfc/rfc9700](https://www.rfc-editor.org/rfc/rfc9700)
- [https://www.rfc-editor.org/rfc/rfc6749](https://www.rfc-editor.org/rfc/rfc6749)

## ความสัมพันธ์กับเรื่องอื่น

[[JWT]] · [[HTTP]] · [[Session Management]]

## แหล่งข้อมูลและการตรวจสอบ

- [เอกสารทางการ](https://www.rfc-editor.org/rfc/rfc6749)
- [ข่าว/รุ่น/มาตรฐาน](https://www.rfc-editor.org/rfc/rfc9700)
- ตรวจลิงก์และสถานะเอกสารเมื่อ **2026-11-20**; หน้านี้ไม่ได้ pin patch version เพราะเอกสารต้นทางอัปเดตต่อเนื่อง

## อ่านเนื้อหาออฟไลน์

หัวข้อเหล่านี้อธิบายแนวคิดและการตัดสินใจที่เกี่ยวข้อง โดยเนื้อหาสำคัญอยู่ใน Vault ไม่ต้องเปิดเว็บเพื่ออ่านพื้นฐาน:

[[OAuth Authorization Code with PKCE]] · [[JWT Validation]] · [[HTTP Request Lifecycle]]
