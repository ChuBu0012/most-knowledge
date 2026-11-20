---
title: "Reka UI"
type: technology
domain: frontend-libraries
technology: "Reka UI"
level: beginner-to-advanced
tags: [technical-knowledge, frontend-libraries, reka-ui]
status: overview
last_verified: 2026-11-20
sources:
  - https://reka-ui.com/docs/overview/introduction
  - https://github.com/unovue/reka-ui/releases
---

# Reka UI

## Overview

ชุด accessible, unstyled primitives สำหรับ Vue ที่ให้ interaction logic แต่เปิดให้กำหนดหน้าตาเอง

## เลือกใช้เมื่อ

ต้องการ custom Vue design system พร้อม accessibility behavior

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

Reka UI 2.11.0 (5 Oct) added Field/Form primitives, TagGroup, and keyboard navigation improvements across listbox/select/tree. It is an unstyled Vue primitive layer: application code owns visual design, while primitives provide interaction and accessibility behavior.

แหล่งยืนยัน snapshot: - [https://github.com/unovue/reka-ui/releases](https://github.com/unovue/reka-ui/releases)
- [https://reka-ui.com/](https://reka-ui.com/)

## ความสัมพันธ์กับเรื่องอื่น

[[Vue]] · [[Tailwind CSS]] · [[DaisyUI]]

## แหล่งข้อมูลและการตรวจสอบ

- [เอกสารทางการ](https://reka-ui.com/docs/overview/introduction)
- [ข่าว/รุ่น/มาตรฐาน](https://github.com/unovue/reka-ui/releases)
- ตรวจลิงก์และสถานะเอกสารเมื่อ **2026-11-20**; หน้านี้ไม่ได้ pin patch version เพราะเอกสารต้นทางอัปเดตต่อเนื่อง

## อ่านเนื้อหาออฟไลน์

หัวข้อเหล่านี้อธิบายแนวคิดและการตัดสินใจที่เกี่ยวข้อง โดยเนื้อหาสำคัญอยู่ใน Vault ไม่ต้องเปิดเว็บเพื่ออ่านพื้นฐาน:

[[Vue Reactivity and Computed State]] · [[Utility-First CSS and Design Tokens]]


## คำสั่งและสูตรใช้งาน

[[Technical-Knowledge/12-Command-Reference/Reka-UI/Reka-UI-Recipes|Reka UI Recipes]] — ตัวอย่าง API/คำสั่งที่ใช้บ่อย

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
