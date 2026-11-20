---
title: Technical Knowledge — Home
type: hub
tags: [technical-knowledge, home]
status: published
last_verified: 2026-11-20
---

# Technical Reference Library

คลังนี้จัด **แหล่งอ้างอิงของทุกหัวข้อ** ใน software development เป็นหลัก: เอกสารทางการ, API/command reference, standards, tutorials, migration guides และ release notes พร้อม link จาก knowledge unit ไปยังแหล่งที่เกี่ยวข้อง. หน้าสรุป/ตัวอย่างใน vault เป็นทางเข้าช่วยเลือกอ่าน; รายละเอียด version-specific ให้ยืนยันจาก reference ต้นทาง.

## ยังไม่แน่ใจว่าจะเริ่มตรงไหน?

- **ทำหน้าเว็บ:** เริ่ม [[Technology-Index#Frontend|Frontend]]; เลือก React ecosystem ถ้าใช้ React, Vue/Nuxt ถ้าใช้ Vue, SvelteKit ถ้าต้องการ Svelte full-stack
- **ทำ API:** เลือก [[Technology-Index#Backend|Backend]] ตามภาษากับ runtime ที่มีอยู่; Go → Gin/Fiber, JS runtimes → Hono/Express/Elysia, Python → FastAPI
- **จัดการข้อมูล:** แยกข้อมูล server/cache (TanStack Query) ออกจาก client UI state (Zustand/Pinia); เลือก ORM หรือ SQL-first ที่ [[Technology-Index#Database-and-data-access|Database]]
- **ตรวจข้อมูล:** ใช้ Zod หรือ validation ในภาษา/framework; เพิ่ม [[Technology-Index#Testing|Testing]] ตามระดับ unit ถึง browser journey
- **จัดระบบ deploy:** [[Technology-Index#Infrastructure|Docker]], Compose, Nginx และ RabbitMQ แก้คนละปัญหา ดู overview ก่อนเลือก
- **แก้ปัญหา Git/Linux/SSH/animation:** ไป [[START-HERE]] ซึ่งเป็นหน้ารวม How-To ของ Vault

## แผนที่

- [[Technology-Index|Technology Index]] — เลือกจากงานและเปิด overview ของแต่ละรายการ
- [[Technical-Knowledge/10-Comparisons/Technology-Selection-Guide|Technology Selection Guide]] — เทียบตัวเลือกตามโจทย์
- [[Knowledge-Map|Knowledge Map]] — ความสัมพันธ์และลำดับพื้นฐาน
- [[Concept-Index|Concept Index]] — เปิดอ่านกลไกย่อยแบบ offline
- [[Technical-Knowledge/13-References/Reference-Catalog|Reference Catalog]] — แหล่งอ้างอิงครบทุก knowledge unit จัดกลุ่มตามชนิดเอกสาร
- [[Command-Finder|Command & API Finder]] — ตัวอย่างคำสั่งใน vault ใช้เป็น index เสริมของแหล่งอ้างอิง
- [[Version-Matrix|Version & Update Tracker]] — วิธีตรวจข้อมูลล่าสุดและสถานะที่ตรวจแล้ว
- [[Glossary|Glossary]] — คำศัพท์ร่วม

## วิธีดูแลความรู้

เริ่มจากหัวข้อที่ต้องการ → เปิด Reference Catalog หรือแหล่งอ้างอิงในหน้านั้น → ตรวจชนิดเอกสารและเวอร์ชัน → ใช้ official API/spec/release notes เป็นหลักเมื่อเลือกวิธีใช้งาน
