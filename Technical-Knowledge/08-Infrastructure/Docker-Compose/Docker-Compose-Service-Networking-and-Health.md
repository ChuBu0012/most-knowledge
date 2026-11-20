---
title: "Docker Compose Service Networking and Health"
type: concept
domain: docker compose
level: intermediate-to-advanced
tags: [docker, compose, networking]
status: researched
last_verified: 2026-11-20
sources:
  - https://docs.docker.com/compose/how-tos/networking/
---

# Docker Compose Service Networking and Health

## Overview

Compose นิยามหลาย service ใน project เดียว; service discovery ทำผ่านชื่อ service บน default network ไม่ใช้ localhost ข้าม container

## กลไกและแนวคิดหลัก

ภายใน container, `localhost` อ้าง container ปัจจุบัน; API ติดต่อ `db:5432` ผ่าน DNS ของ Compose network. `depends_on` คุมลำดับเริ่มต้น แต่ไม่ได้รับประกัน dependency พร้อมรับ traffic หากไม่มี health condition และ retry. Named volume เก็บข้อมูลข้าม container recreation

## ตัวอย่าง

```yaml
services:
  api:
    build: .
    depends_on:
      db:
        condition: service_healthy
  db:
    image: postgres:18
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U app"]
```

ตัวอย่างเป็น schematic ที่สื่อหลักการ; ตรวจ syntax และ config ให้ตรงกับ version/runtime ที่ใช้งานก่อนนำไป deploy

## จุดพลาดและข้อควรระวัง

port ที่ publish สู่ host ไม่ใช่วิธีติดต่อระหว่าง services; environment variables อาจมี secret และ compose file ไม่ใช่ secret manager; container restart policy ไม่แก้ bug ของ process

## แนวทางปฏิบัติ

ให้ service retry dependency ด้วย backoff, ใช้ healthcheck สะท้อน readiness, persistent volume สำหรับ state และแยก internal network จาก published ports

## ความสัมพันธ์

[[Docker]] · [[Redis]] · [[RabbitMQ]] · [[Database Connection Pooling]]

## แหล่งอ้างอิง

- [เอกสาร/มาตรฐานต้นทาง](https://docs.docker.com/compose/how-tos/networking/)
- เนื้อหาสรุปและตัวอย่างด้านบนเก็บใน Vault เพื่ออ่าน offline; ตรวจ version-specific details ก่อนใช้กับระบบจริง
