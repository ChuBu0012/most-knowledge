---
title: "Docker"
type: technology
domain: infrastructure
technology: "Docker"
level: beginner-to-advanced
tags: [technical-knowledge, infrastructure, docker]
status: overview
last_verified: 2026-11-20
sources:
  - https://docs.docker.com/
  - https://docs.docker.com/engine/release-notes/
---

# Docker

## Overview

แพลตฟอร์มสร้างและรัน container images เพื่อบรรจุแอปและ dependencies ให้สภาพแวดล้อมทำซ้ำได้

## เลือกใช้เมื่อ

ต้องการ dev/test/deploy ที่ใกล้เคียงกันและแยก process ด้วย container

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

Use the current Docker Engine and BuildKit documentation as the version source; behavior is now shaped by BuildKit builders, cache exporters, and Compose v5. Build reproducibly with pinned base images, explicit build contexts, and secrets mounts rather than build arguments for credentials.

แหล่งยืนยัน snapshot: - [https://docs.docker.com/engine/release-notes/](https://docs.docker.com/engine/release-notes/)
- [https://docs.docker.com/build/](https://docs.docker.com/build/)

## ความสัมพันธ์กับเรื่องอื่น

[[Docker Compose]] · [[Nginx]] · [[Redis]]

## แหล่งข้อมูลและการตรวจสอบ

- [เอกสารทางการ](https://docs.docker.com/)
- [ข่าว/รุ่น/มาตรฐาน](https://docs.docker.com/engine/release-notes/)
- ตรวจลิงก์และสถานะเอกสารเมื่อ **2026-11-20**; หน้านี้ไม่ได้ pin patch version เพราะเอกสารต้นทางอัปเดตต่อเนื่อง

## อ่านเนื้อหาออฟไลน์

หัวข้อเหล่านี้อธิบายแนวคิดและการตัดสินใจที่เกี่ยวข้อง โดยเนื้อหาสำคัญอยู่ใน Vault ไม่ต้องเปิดเว็บเพื่ออ่านพื้นฐาน:

[[Docker Image Layers and Reproducible Builds]] · [[Docker Compose Service Networking and Health]]
