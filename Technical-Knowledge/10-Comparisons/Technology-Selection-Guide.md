---
title: Technology Selection Guide
type: comparison
tags: [technical-knowledge, decision-guide, comparison]
status: published
last_verified: 2026-11-20
---

# Technology Selection Guide

เริ่มจากภาษาที่ทีมใช้, deployment environment, ความซับซ้อนของปัญหา และความสามารถในการดูแลระบบ อย่าเลือกจาก benchmark หรือความนิยมเพียงอย่างเดียว

## Frontend

| ถ้าต้องการ | เริ่มดู | เหตุผล/ข้อแลกเปลี่ยน |
|---|---|---|
| React ecosystem และ UI แบบยืดหยุ่น | [[React]] | ecosystem ใหญ่ ต้องเลือก router/data/form tools เพิ่มตามโจทย์ |
| React พร้อม SSR/full-stack conventions | [[Next.js with TypeScript]] | รวม routing/rendering/server patterns แต่ผูกกับ framework conventions มากขึ้น |
| React แบบ Vite และ route-centric data | [[React Router Framework]] | เหมาะกับ SPA/SSR ผ่าน framework mode และใช้ React ecosystem เดิม |
| Vue และ incremental adoption | [[Vue]] | เริ่มเล็กได้; เพิ่ม [[Pinia]] เมื่อ shared state เริ่มซับซ้อน |
| Vue SSR/full-stack | [[Nuxt]] | มี conventions และ server engine; ต้องเข้าใจ rendering/runtime |
| Svelte full-stack | [[SvelteKit]] | framework ของ Svelte ครอบคลุม routing/rendering/actions |
| build tooling สำหรับแอป frontend ที่เลือกเอง | [[Vite]] | dev/build tool ไม่ใช่ UI framework หรือ full-stack framework |

## Backend

| สภาพแวดล้อม/ความต้องการ | เริ่มดู | ควรพิจารณา |
|---|---|---|
| Go และ framework ทั่วไป | [[Gin]] | ecosystem/รูปแบบมาตรฐาน; เปรียบเทียบกับ fasthttp ของ Fiber |
| Go และ API คล้าย Express | [[Fiber]] | เช็ก fasthttp compatibility กับ middleware/มาตรฐาน net/http ที่ต้องใช้ |
| JavaScript หลาย runtime/edge | [[Hono]] | Web Standards API และ portability เป็นจุดเด่น |
| Node.js ecosystem แบบ minimal | [[Express]] | ยืดหยุ่นสูง จึงต้องกำหนดโครงสร้างและ security policy เอง |
| Bun + type-first API | [[Elysia]] | เลือกเมื่อรับ runtime coupling กับ Bun ได้ |
| Python API และ OpenAPI | [[FastAPI]] | ใช้ type hints/schema docs; วางแผน dependency และ async I/O ให้เหมาะ |

## State, data และ forms

- Remote/server state: เริ่มจาก [[TanStack-Query]]; อย่าจำลอง cache/refetch เองโดยไม่จำเป็น
- UI/client state: React ใช้ [[Zustand]] เมื่อแชร์ state แล้ว; Vue ใช้ [[Pinia]]
- Form ใน React: [[React-Hook-Form]] มี ecosystem กว้าง; [[TanStack-Form]] เป็น headless ทางเลือกและต้องเช็กสถานะ major/alpha ก่อนใช้งาน
- Form ใน Vue: [[VeeValidate]]
- Runtime validation: [[Zod]] เมื่อข้อมูลข้าม trust boundary
- Data table/list: [[TanStack-Table]] ให้ logic ไม่ให้ visual UI; [[TanStack-Virtual]] ช่วยรายการขนาดใหญ่
- Database: [[Prisma]]/[[GORM]] ให้ abstraction ระดับ model; [[sqlc]] ให้เขียน SQL เองและสร้าง typed code

## Deploy และ asynchronous work

- พัฒนา/แพ็ก environment ซ้ำได้: [[Docker]]; รันหลาย service ใน dev: [[Docker-Compose]]
- รับ request หน้า backend/serve static/load balance: [[Nginx]]
- งาน async ที่ต้อง queue, routing และ acknowledgement: [[RabbitMQ]]; cache/low-latency data structures: [[Redis]]

## ข้อควรจำเรื่อง Security

[[OAuth-2.0]] เป็น authorization framework ส่วน [[JWT]] เป็น token format; ไม่จำเป็นต้องใช้ JWT ทุกระบบ และการมี JWT ไม่ได้ทำให้ระบบปลอดภัยโดยอัตโนมัติ

## อ่านต่อ

- [[Technical-Knowledge/00-Home/Technology-Index|Technology Index]]
- [[Technical-Knowledge/00-Home/Knowledge-Map|Knowledge Map]]
- [[Technical-Knowledge/00-Home/Version-Matrix|ตรวจเวอร์ชันและอัปเดต]]
