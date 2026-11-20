---
title: "Playwright"
type: technology
domain: testing
technology: "Playwright"
level: beginner-to-advanced
tags: [technical-knowledge, testing, playwright]
status: overview
last_verified: 2026-11-20
sources:
  - https://playwright.dev/docs/intro
  - https://playwright.dev/docs/release-notes
---

# Playwright

## Overview

เครื่องมือ browser automation และ end-to-end testing รองรับ Chromium, Firefox และ WebKit

## เลือกใช้เมื่อ

ทดสอบ user journey จริงข้าม browser และตรวจ regression ของ UI

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

[[Vitest]] · [[SvelteKit]] · [[React]]

## แหล่งข้อมูลและการตรวจสอบ

- [เอกสารทางการ](https://playwright.dev/docs/intro)
- [ข่าว/รุ่น/มาตรฐาน](https://playwright.dev/docs/release-notes)
- ตรวจลิงก์และสถานะเอกสารเมื่อ **2026-11-20**; หน้านี้ไม่ได้ pin patch version เพราะเอกสารต้นทางอัปเดตต่อเนื่อง

## อ่านเนื้อหาออฟไลน์

หัวข้อเหล่านี้อธิบายแนวคิดและการตัดสินใจที่เกี่ยวข้อง โดยเนื้อหาสำคัญอยู่ใน Vault ไม่ต้องเปิดเว็บเพื่ออ่านพื้นฐาน:

[[Playwright Locators and Auto-Waiting]] · [[Unit Integration and End-to-End Tests]] · [[Cookie and Session Security]]

## Update snapshot — 2026-11-20

Release notes ถึง 1.65: runner รองรับ Bun พร้อมข้อจำกัดบางอย่าง; Node 20 ไม่อยู่ใน support test แล้ว. อ่าน breaking changes เรื่อง cookies, proxy credentials, TS class fields และ inert elements จาก [release notes](https://playwright.dev/docs/release-notes).

## แนวคิดและคู่มือภายใน Vault

[[Playwright Locators and Auto-Waiting]] · [[Unit Integration and End-to-End Tests]] · [[Technical-Knowledge/00-Home/Recent-Updates|สรุปอัปเดตทั้งหมด]]


## คำสั่งและสูตรใช้งาน

[[Playwright Recipes]] — task-first walkthrough สำหรับการใช้งานจริง

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
