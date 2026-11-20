---
title: "React"
type: technology
domain: frontend
technology: "React"
level: beginner-to-advanced
tags: [technical-knowledge, frontend, react]
status: overview
last_verified: 2026-11-20
sources:
  - https://react.dev/learn
  - https://react.dev/blog
---

# React

## Overview

ไลบรารีสร้าง UI แบบ component โดยอธิบายหน้าจอจาก state และให้ React จัดการการ render

## เลือกใช้เมื่อ

UI ที่มี interaction และต้องการ ecosystem component ขนาดใหญ่

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

[[React with TypeScript]] · [[Next.js with TypeScript]] · [[Zustand]] · [[TanStack Query]]

## แหล่งข้อมูลและการตรวจสอบ

- [เอกสารทางการ](https://react.dev/learn)
- [ข่าว/รุ่น/มาตรฐาน](https://react.dev/blog)
- ตรวจลิงก์และสถานะเอกสารเมื่อ **2026-11-20**; หน้านี้ไม่ได้ pin patch version เพราะเอกสารต้นทางอัปเดตต่อเนื่อง

## อ่านเนื้อหาออฟไลน์

หัวข้อเหล่านี้อธิบายแนวคิดและการตัดสินใจที่เกี่ยวข้อง โดยเนื้อหาสำคัญอยู่ใน Vault ไม่ต้องเปิดเว็บเพื่ออ่านพื้นฐาน:

[[React Rendering Model]] · [[React State and Batching]] · [[React Component Identity and Keys]] · [[React Effect Synchronization]] · [[React Component Composition]] · [[React Server and Client Components]]

## Update snapshot — 2026-11-20

19.3 stable (9 Sep 2026): View Transitions และ Fragment Refs stable; Server Components สามารถ render Context จาก client module ได้ และ Strict Mode ตรวจ Effects ช่วง hydration เพิ่มเติม. ให้อ่าน [release note](https://react.dev/blog/2026/09/09/react-19-3) ก่อนใช้ APIs ใหม่.

## แนวคิดและคู่มือภายใน Vault

[[React Rendering Model]] · [[React Effect Synchronization]] · [[React Server and Client Components]] · [[Technical-Knowledge/00-Home/Recent-Updates|สรุปอัปเดตทั้งหมด]]


## คำสั่งและสูตรใช้งาน

[[React Recipes]] — ค้น API/คำสั่งจากงานที่ต้องทำ พร้อมตัวอย่างและข้อควรระวัง

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
