---
title: "RabbitMQ"
type: technology
domain: infrastructure
technology: "RabbitMQ"
level: beginner-to-advanced
tags: [technical-knowledge, infrastructure, rabbitmq]
status: overview
last_verified: 2026-11-20
sources:
  - https://www.rabbitmq.com/docs
  - https://www.rabbitmq.com/changelog.html
  - https://www.rabbitmq.com/release-information
---

# RabbitMQ

## Overview

message broker รองรับ queues, exchanges, routing และ acknowledgements สำหรับงาน asynchronous

## เลือกใช้เมื่อ

ต้องแยกงานเบื้องหลังหรือสื่อสารระหว่าง service แบบทนต่อการหยุดชั่วคราว

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

[[Go]] · [[Docker Compose]] · [[Redis]]

## แหล่งข้อมูลและการตรวจสอบ

- [เอกสารทางการ](https://www.rabbitmq.com/docs)
- [ข่าว/รุ่น/มาตรฐาน](https://www.rabbitmq.com/changelog.html)
- ตรวจลิงก์และสถานะเอกสารเมื่อ **2026-11-20**; หน้านี้ไม่ได้ pin patch version เพราะเอกสารต้นทางอัปเดตต่อเนื่อง

## อ่านเนื้อหาออฟไลน์

หัวข้อเหล่านี้อธิบายแนวคิดและการตัดสินใจที่เกี่ยวข้อง โดยเนื้อหาสำคัญอยู่ใน Vault ไม่ต้องเปิดเว็บเพื่ออ่านพื้นฐาน:

[[RabbitMQ Acknowledgements and Redelivery]] · [[Database-Transactions]] · [[Go Context]]

## Update snapshot — 2026-11-20

RabbitMQ 4.4.1 (16 Nov 2026) เพิ่ม quorum queue delayed/deferred messages, Erlang 29, post-quantum TLS และ native STOMP. ตรวจ [release information](https://www.rabbitmq.com/release-information) และ client protocol support.

## แนวคิดและคู่มือภายใน Vault

[[RabbitMQ Acknowledgements and Redelivery]] · [[Database-Transactions]] · [[Technical-Knowledge/00-Home/Recent-Updates|สรุปอัปเดตทั้งหมด]]


## คำสั่งและสูตรใช้งาน

[[RabbitMQ Recipes]] — task-first API และคำสั่งที่ใช้บ่อย

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
