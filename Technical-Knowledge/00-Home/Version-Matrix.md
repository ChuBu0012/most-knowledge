---
title: Version and Update Tracker
type: reference
tags: [technical-knowledge, versions, maintenance]
status: published
last_verified: 2026-11-20
---

# Version & Update Tracker

## สถานะการตรวจ

ตรวจแหล่งทางการและลิงก์รุ่นของทุก overview ในคลัง ณ **2026-11-20**. เพราะรายการครอบคลุมหลายสิบโครงการที่ปล่อยรุ่นถี่ ตารางนี้ใช้ official release/changelog เป็นแหล่งค่ารุ่นล่าสุด แทนการฝังเลข patch ที่จะหมดอายุเร็ว

| รายการ | ข้อสังเกต ณ วันตรวจ | แหล่งตรวจต่อ |
|---|---|---|
| React | React 19.3 ประกาศ stable วันที่ 2026-09-09 รวม View Transitions และ Fragment Refs | [React 19.3](https://react.dev/blog/2026/09/09/react-19-3) · [[React]] |
| SvelteKit | SvelteKit 3 และ `sv` 1.0 ประกาศ 2026-10-01; ตรวจ migration ก่อนใช้คู่มือเก่า | [Svelte blog](https://svelte.dev/blog) · [[SvelteKit]] |
| Vite | Vite 8 stable ประกาศ 2026-03-12; ตรวจ plugin compatibility | [Vite 8](https://vite.dev/blog/announcing-vite8) · [[Vite]] |
| TanStack Form | Form v2 อยู่สถานะ alpha ตามประกาศ 2026-08-06; อย่าสับสนกับ stable v1 ใน production | [Form v2 alpha](https://tanstack.com/blog/announcing-tanstack-form-v2-alpha) · [[TanStack-Form]] |
| TanStack Table | เอกสารปัจจุบันมีแนวทาง migration จาก v8 ไป v9; ตรวจ migration guide ก่อนอัปเกรด | [Table docs](https://tanstack.com/table/latest/docs/overview) · [[TanStack-Table]] |
| OAuth 2.0 | ใช้ RFC 9700 เป็น security best current practice เพิ่มเติมจาก RFC 6749 | [RFC 9700](https://www.rfc-editor.org/rfc/rfc9700) · [[OAuth-2.0]] |
| เทคโนโลยีอื่น | ใช้ official docs/changelog ที่ฝังในแต่ละหน้า overview; ไม่ pin patch version ในสารบัญ | [[Technology-Index]] |

## วิธีอัปเดตความรู้

1. ก่อนเริ่มงาน/อัปเกรด เปิดเอกสารทางการและ release notes ของ dependency ที่ติดตั้งจริง
2. บันทึก major/minor ที่มีผลต่อเนื้อหาในหน้า concept และเติมวันที่ `last_verified`
3. แยก stable, beta, alpha และ experimental ให้ชัด; ห้ามนำ API จากคนละ major มารวมโดยไม่บอก
4. ลิงก์นี้เป็น tracker สำหรับเริ่มตรวจ ไม่ได้หมายความว่าได้ตรวจทุก API ย่อยหรือทุก patch release
