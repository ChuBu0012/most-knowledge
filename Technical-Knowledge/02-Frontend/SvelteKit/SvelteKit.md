---
title: "SvelteKit"
type: technology
domain: frontend
technology: "SvelteKit"
level: beginner-to-advanced
tags: [technical-knowledge, frontend, sveltekit]
status: overview
last_verified: 2026-11-20
sources:
  - https://svelte.dev/docs/kit/introduction
  - https://svelte.dev/blog
---

# SvelteKit

## Overview

Svelte application framework ที่จัดการ routing, server rendering, form actions และ deployment adapters

## เลือกใช้เมื่อ

เว็บ Svelte ตั้งแต่ static site ถึง server-rendered app

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

[[Vite]] · [[TypeScript]] · [[Playwright]]

## แหล่งข้อมูลและการตรวจสอบ

- [เอกสารทางการ](https://svelte.dev/docs/kit/introduction)
- [ข่าว/รุ่น/มาตรฐาน](https://svelte.dev/blog)
- ตรวจลิงก์และสถานะเอกสารเมื่อ **2026-11-20**; หน้านี้ไม่ได้ pin patch version เพราะเอกสารต้นทางอัปเดตต่อเนื่อง

## อ่านเนื้อหาออฟไลน์

หัวข้อเหล่านี้อธิบายแนวคิดและการตัดสินใจที่เกี่ยวข้อง โดยเนื้อหาสำคัญอยู่ใน Vault ไม่ต้องเปิดเว็บเพื่ออ่านพื้นฐาน:

[[Svelte Runes and Reactivity]] · [[Vite Development and Production Builds]] · [[Playwright Locators and Auto-Waiting]]

## Update snapshot — 2026-11-20

SvelteKit 3 stable และ `sv` 1.0 ตั้งแต่ 1 Oct 2026; migration command `npx sv migrate sveltekit-3` ช่วยอัปเดตได้บางส่วน แต่สร้าง TODO สำหรับ breaking changes ที่ต้องแก้เอง. อ่าน [SvelteKit 3 migration announcement](https://svelte.dev/blog/sveltekit-3-is-here).

## แนวคิดและคู่มือภายใน Vault

[[Svelte Runes and Reactivity]] · [[Vite Development and Production Builds]] · [[Technical-Knowledge/00-Home/Recent-Updates|สรุปอัปเดตทั้งหมด]]
