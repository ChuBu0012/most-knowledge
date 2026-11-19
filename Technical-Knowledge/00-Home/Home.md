---
title: Technical Knowledge — Home
type: hub
tags: [technical-knowledge, home]
status: published
last_verified: 2026-11-20
---

# Technical Knowledge

คลังความรู้ด้าน software development ที่จัดตามงานและโดเมน เนื้อหาเก็บเป็น Markdown เพื่ออ่าน offline ได้; external links ใช้ตรวจเวอร์ชันและรายละเอียดล่าสุด

## ยังไม่แน่ใจว่าจะเริ่มตรงไหน?

- **ทำหน้าเว็บ:** เริ่ม [[Technology-Index#Frontend|Frontend]]; เลือก React ecosystem ถ้าใช้ React, Vue/Nuxt ถ้าใช้ Vue, SvelteKit ถ้าต้องการ Svelte full-stack
- **ทำ API:** เลือก [[Technology-Index#Backend|Backend]] ตามภาษากับ runtime ที่มีอยู่; Go → Gin/Fiber, JS runtimes → Hono/Express/Elysia, Python → FastAPI
- **จัดการข้อมูล:** แยกข้อมูล server/cache (TanStack Query) ออกจาก client UI state (Zustand/Pinia); เลือก ORM หรือ SQL-first ที่ [[Technology-Index#Database-and-data-access|Database]]
- **ตรวจข้อมูล:** ใช้ Zod หรือ validation ในภาษา/framework; เพิ่ม [[Technology-Index#Testing|Testing]] ตามระดับ unit ถึง browser journey
- **จัดระบบ deploy:** [[Technology-Index#Infrastructure|Docker]], Compose, Nginx และ RabbitMQ แก้คนละปัญหา ดู overview ก่อนเลือก
- **แก้ปัญหา Git/Linux/SSH/animation:** ไป [[START-HERE]] ซึ่งเป็นหน้ารวม How-To ของ Vault

## แผนที่

- [[Technology-Index|Technology Index]] — เลือกจากงานและเปิด overview ของแต่ละรายการ
- [[10-Comparisons/Technology-Selection-Guide|Technology Selection Guide]] — เทียบตัวเลือกตามโจทย์
- [[Knowledge-Map|Knowledge Map]] — ความสัมพันธ์และลำดับพื้นฐาน
- [[Version-Matrix|Version & Update Tracker]] — วิธีตรวจข้อมูลล่าสุดและสถานะที่ตรวจแล้ว
- [[Glossary|Glossary]] — คำศัพท์ร่วม

## วิธีดูแลความรู้

เริ่มจาก overview → เพิ่ม atomic concept เมื่อมีคำถามหรือใช้งานจริง → เชื่อมด้วย wikilinks → อ้างอิง official docs และระบุ `last_verified` ทุกครั้งที่ทบทวน
