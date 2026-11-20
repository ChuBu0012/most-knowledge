---
title: Concept Index
type: index
tags: [technical-knowledge, index, concepts]
status: published
last_verified: 2026-11-20
---

# Concept Index

รายการ knowledge units ที่อ่านได้ในเครื่อง เริ่มจากแนวคิดที่อธิบายกลไก แล้วตามลิงก์ไปยัง implementation/technology ที่ใช้จริง. ตอนนี้มี **74 concept notes** นอกเหนือจาก technology overviews.

## HTTP

- [[HTTP]] — พื้นฐานโปรโตคอล request/response ที่ใช้สื่อสารระหว่าง client และ server บนเว็บ
- [[HTTP Request Lifecycle]] — วงจร request อธิบายการเดินทางจาก client ผ่าน DNS/TCP/TLS, proxy, router และ handler ไปสู่ response

## Programming

- [[JavaScript Closures]] — closure คือฟังก์ชันพร้อม lexical environment ที่สร้างฟังก์ชันนั้น ทำให้ฟังก์ชันเก็บการเข้าถึงค่าจากขอบเขตเดิมได้
- [[JavaScript Error Handling]] — error handling แบ่ง failure ที่คาดไว้ให้ caller จัดการ ออกจาก bug ที่ควรพบระหว่างพัฒนา
- [[JavaScript Execution Model]] — การเข้าใจ execution model ช่วยอธิบายว่าทำไมโค้ด synchronous จึงบล็อกงานอื่น และทำไม async callback จึงทำงานภายหลัง
- [[JavaScript Modules]] — ES modules แบ่งโปรแกรมเป็นไฟล์ที่ export/import bindings อย่างชัดเจน ช่วยควบคุม dependency และเปิดโอกาสให้ tree-shaking
- [[JavaScript Promises]] — Promise แทนผลลัพธ์ของงานที่ยังไม่เสร็จหรืออาจล้มเหลว ช่วยต่อ asynchronous computation โดยไม่ซ้อน callback

## SQL

- [[Database Transactions]] — transaction ทำให้หลาย database operations เป็นหน่วยเดียวที่สำเร็จหรือย้อนกลับร่วมกัน
- [[SQL]] — ภาษาเชิงประกาศสำหรับอ่านและเปลี่ยนข้อมูลใน relational database
- [[SQL Indexes and Query Plans]] — index เป็นโครงสร้างค้นหาที่แลกพื้นที่และค่าใช้จ่ายตอนเขียนเพื่อเร่ง query บางรูปแบบ

## Type System

- [[TypeScript Generics]] — generics สร้าง function/type ที่ทำงานกับหลายชนิดข้อมูลโดยรักษาความสัมพันธ์ของ input กับ output
- [[TypeScript Structural Types]] — ระบบ structural typing ตัดสินความเข้ากันได้จากรูปร่างของสมาชิก ไม่ใช่ชื่อ class/type ที่ประกาศ
- [[TypeScript Type Narrowing]] — narrowing ใช้ control flow และการตรวจ runtime ลด union type ให้แคบลงในแต่ละ branch

## Next.js

- [[Next.js Cache Boundaries and Revalidation]] — cache ใน Next.js มีหลายชั้น; ต้องรู้ว่า cache อะไร อยู่ที่ไหน และข้อมูลของ user คนใดจึงจะไม่รั่วข้าม request

## Nuxt

- [[Nuxt Data Fetching and Request Context]] — Nuxt มี composables สำหรับโหลดข้อมูลใน lifecycle ที่รองรับ SSR, hydration และ deduplication; เลือกให้ตรงว่า data ต้องอยู่ฝั่ง server, client หรือทั้งสอง

## React

- [[React Component Composition]] — composition ใช้ประกอบ component เล็กเป็น tree และส่งความรับผิดชอบ/เนื้อหาผ่าน props แทนการสร้าง component ที่รู้จักทั้งแอป
- [[React Component Identity and Keys]] — ตำแหน่ง component และ `key` กำหนดว่า React มอง UI element เป็น instance เดิมหรือ instance ใหม่ จึงมีผลต่อการคง/reset state
- [[React Effect Synchronization]] — Effect เชื่อม component กับระบบภายนอกที่ React ไม่ได้ควบคุม เช่น subscription, browser API หรือ third-party widget
- [[React Rendering Model]] — React render คือการเรียก component เพื่อคำนวณคำอธิบาย UI จาก props, state และ context ในรอบนั้น ไม่ใช่คำสั่งวาด DOM โดยตรง
- [[React Server and Client Components]] — Server Components และ Client Components แบ่งงาน render ระหว่าง server กับ browser; boundary มีผลต่อ code ที่ส่งไป client และ capabilities ที่ใช้ได้
- [[React State and Batching]] — state คือข้อมูลที่ React เก็บข้าม render; ทุก render อ่าน snapshot ของ state ชุดหนึ่ง
- [[React TypeScript Props and Events]] — กำหนด component contract ผ่าน props types และให้ DOM event types อนุมานจาก element ที่ใช้ ลดการ cast และทำให้ refactor ปลอดภัย

## SvelteKit

- [[Svelte Runes and Reactivity]] — Svelte compiler แปลง component ให้ updates ทำงานตาม reactive dependencies; Svelte 5 ใช้ runes แสดง state/derived/effect อย่างชัดเจน
- [[SvelteKit Load Functions and Form Actions]] — SvelteKit ใช้ `load` เติมข้อมูลตาม route และ form actions รับ mutation แบบ progressive enhancement; server/client load ต่างกันเรื่อง trust และ capabilities

## Vite

- [[Vite Development and Production Builds]] — Vite ใช้ dev server ที่เสิร์ฟ source modules แบบ ESM และทำ production build ผ่าน bundler เพื่อสร้าง assets ที่ optimize แล้ว

## Vue

- [[Vue Composables]] — composable คือ function ที่ใช้ Composition API เพื่อรวม stateful behavior และให้ component นำไปประกอบใช้ซ้ำ
- [[Vue Reactivity and Computed State]] — Vue reactivity ติดตามการอ่าน reactive state ระหว่างการประมวลผล แล้ว trigger effects เมื่อ property ที่อ่านถูกเปลี่ยน
- [[Vue TypeScript Props and Emits]] — Vue SFC สามารถอนุมาน props/emits ผ่าน `defineProps` และ `defineEmits` ทำให้ component contract อยู่ใกล้ template

## 03 Frontend Libraries

- [[Browser Form State]] — ฟอร์มมี state มากกว่าค่า input: touched/dirty, validation, submission, server errors และสถานะระหว่างส่ง

## Pinia

- [[Pinia Store State Actions and Getters]] — Pinia store รวม state, actions และ getters ภายใต้ id ที่เรียกซ้ำจาก component/composable ได้; Vue reactivity ทำให้ UI ติดตามการเปลี่ยน state

## React Hook Form

- [[React Hook Form Registration and Validation]] — React Hook Form ใช้ form control/registration เก็บค่าจาก inputs โดยลดการ rerender ทั้งฟอร์ม; resolver เชื่อม schema validation

## Tailwind CSS

- [[Utility-First CSS and Design Tokens]] — utility-first CSS เขียน style จากชุด class เล็ก ๆ ใน markup ส่วน design tokens ทำให้สี, spacing, type และ radius มีค่ากลางสม่ำเสมอ

## TanStack

- [[List Virtualization and Windowing]] — Windowing render เฉพาะ rows/items ที่อยู่ใกล้ viewport พร้อม spacer/positioning เพื่อให้ list ใหญ่มีจำนวน DOM nodes คงที่
- [[TanStack Query Cache Lifecycle]] — TanStack Query เก็บผล query ตาม query key และจัดการ freshness, refetch, retries, observers และ invalidation แทนการผูก remote data กับ UI state เอง
- [[TanStack Router Loaders and URL State]] — Router loader ผูกการโหลดข้อมูลกับ route match และ URL state ช่วยให้ deep link, back/forward และ refresh สะท้อนหน้าจอเดียวกัน
- [[TanStack Table Row Models and Features]] — TanStack Table แยก core row model ออกจาก feature row models เพื่อคำนวณ filter/sort/group/pagination โดยไม่กำหนด markup

## VeeValidate

- [[VeeValidate Form and Field Lifecycle]] — VeeValidate ติดตามค่า/touched/errors/submission ต่อ form และ field; lifecycle ช่วยให้ field เพิ่ม/ถอดตาม conditional UI ได้

## Zod

- [[Zod Runtime Validation]] — Zod schema ใช้ parse ข้อมูลที่ type checker ไม่สามารถรับรองตอน runtime และสร้าง TypeScript type จาก schema ได้

## Zustand

- [[Zustand Store Selectors and Persistence]] — Zustand store เก็บ client state นอก component; component subscribe เฉพาะ selected slice เพื่อหลีกเลี่ยง render ที่ไม่เกี่ยวข้อง

## Bun

- [[Bun Runtime Compatibility and Deployment]] — Bun รวม JavaScript runtime, package manager, test runner และ bundler; การแทน Node.js ต้องตรวจ API, package/native dependency และ operational behavior ทีละส่วน

## Elysia

- [[Elysia Schemas Plugins and Type Inference]] — Elysia ผูก route schema กับ validation, response typing และ inferred client types; plugin encapsulation ช่วยแบ่งขอบเขต dependency/routes

## Express

- [[Express Middleware Ordering and Errors]] — Express application คือ stack ของ middleware/route handlers; ลำดับ `app.use()` เป็นส่วนหนึ่งของ behavior และ security

## FastAPI

- [[FastAPI Dependency Injection and Lifetimes]] — Dependency system สร้าง dependency graph จาก endpoint parameters ให้แชร์ auth, db session, config และ resource cleanup โดยประกาศผ่าน type hints

## Go

- [[Go Channels]] — channel เป็น typed conduit สำหรับส่งค่าและประสานงานระหว่าง goroutines
- [[Go Context]] — context ส่ง deadline, cancellation และ request-scoped metadata ผ่าน call chain เพื่อให้การทำงานหยุดตามต้นทางได้
- [[Go Error Handling]] — Go ใช้ error เป็นค่าที่ส่งกลับอย่างชัดแจ้ง ทำให้เส้นทาง failure ปรากฏใน control flow
- [[Go Goroutines]] — goroutine คือหน่วย execution เบาที่ Go runtime จัดการ เหมาะกับงาน concurrent ที่ต้องรอ I/O หรือประมวลผลแยกกัน
- [[Go HTTP Handler Boundaries]] — HTTP handler เป็น boundary ระหว่าง untrusted request กับ domain logic; แยก parse/validate, authorization, use case และ response mapping

## Hono

- [[Hono Middleware and Request Validation]] — Hono ใช้ middleware chain รอบ handler; request validation ควรเกิดก่อน logic ที่พึ่งข้อมูลนั้น และ middleware order มีผลต่อ auth/logging/errors

## JavaScript Runtime

- [[Node.js]] — JavaScript runtime ฝั่ง server ที่สร้างบน V8 และ event loop พร้อม APIs สำหรับ I/O

## Nitro

- [[Nitro]] — server engine ของ Nuxt ที่จัดการ server routes, presets และ deployment targets

## Python

- [[Python]] — ภาษาโปรแกรม general-purpose ที่อ่านง่ายและมี ecosystem สำหรับ API, automation และ data work

## 05 Database

- [[Database Connection Pooling]] — connection pool reuse database connections เพื่อเลี่ยง handshake/auth overhead และจำกัดจำนวน session ที่ backend เปิดพร้อมกัน
- [[PostgreSQL]] — relational database ที่รองรับ SQL, transactions, constraints และ extensible data types

## GORM

- [[GORM Transactions and Associations]] — GORM map struct models ไป table/associations และให้ CRUD API; transaction boundary ควรตาม invariant ทางธุรกิจ ไม่ใช่จำนวน method calls

## Prisma

- [[Prisma Data Model and Migration Safety]] — Prisma model/schema เป็น contract ระหว่าง application types กับ relational/document data; migration เปลี่ยน schema จริงและอาจทำลายข้อมูล

## Redis

- [[Redis Cache-Aside]] — cache-aside ให้ application อ่าน cache ก่อน; เมื่อ miss จึงอ่าน primary database แล้วเติม cache พร้อม expiry
- [[Redis Persistence and Durability Choices]] — Redis มักถูกใช้เป็น cache แต่รองรับ persistence modes ที่ให้ durability/performance trade-offs ต่างกัน; การเลือกต้องระบุว่า data loss ยอมรับได้เท่าไร

## sqlc

- [[sqlc Query Contracts and Generated Code]] — sqlc แปลง SQL ที่เขียนไว้เป็น typed methods; SQL ยังคงเป็น source of truth จึงตรวจ query plan และ database semantics ได้ตรง

## 06 Security

- [[Cookie and Session Security]] — session cookie เป็น bearer credential ที่เชื่อม browser กับ server-side session; ผู้ขโมย cookie อาจสวมรอยผู้ใช้ได้
- [[HTTP Authentication]] — กลไกยืนยันตัวตนระดับ HTTP เช่น Basic/Bearer challenge และ authentication headers
- [[JWT Validation]] — การใช้ JWT อย่างปลอดภัยต้อง verify cryptographic signature และ claims ที่แอปเชื่อถือ ไม่ใช่แค่ decode JSON
- [[OAuth Authorization Code with PKCE]] — flow สำหรับให้ client ขอ authorization ผ่าน authorization server โดยไม่รับรหัสผ่านของผู้ใช้โดยตรง
- [[Session Management]] — วิธีรักษาสถานะผู้ใช้ข้าม HTTP requests โดยใช้ session identifier และ server-side state

## 07 Testing

- [[Unit Integration and End-to-End Tests]] — test levels ต่างกันตามขอบเขต dependency ที่จริง: unit ทดสอบ logic แคบ, integration ทดสอบ collaboration จริง, end-to-end ทดสอบ journey ผ่านระบบประกอบ

## Go Testing

- [[Go Table-Driven Tests]] — table-driven test ใช้ cases ที่ระบุ input, expected output และชื่อกรณี เพื่อทดสอบ behavior หลายขอบเขตด้วยโครงสร้างเดียว

## Playwright

- [[Playwright Locators and Auto-Waiting]] — Locator คือ query ที่ resolve element ณ เวลาสั่ง action/assertion; auto-wait ช่วยรอ actionability และ condition โดยไม่ต้อง sleep

## Docker

- [[Docker Image Layers and Reproducible Builds]] — image เป็น filesystem layers แบบ immutable พร้อม metadata; container เพิ่ม writable layer ตอนรัน

## Docker Compose

- [[Docker Compose Service Networking and Health]] — Compose นิยามหลาย service ใน project เดียว; service discovery ทำผ่านชื่อ service บน default network ไม่ใช้ localhost ข้าม container

## Nginx

- [[Nginx Reverse Proxy Request Flow]] — reverse proxy รับ request จาก client แล้วส่งต่อ backend; ใช้ TLS termination, routing, buffering และ load balancing ได้

## RabbitMQ

- [[RabbitMQ Acknowledgements and Redelivery]] — broker delivery เป็น asynchronous handoff; publisher confirm และ consumer acknowledgement เป็นคนละทิศทางและคนละหลักประกัน

## API Design

- [[HTTP Semantics and REST]] — การออกแบบ HTTP API ใช้ semantics ของ method, status และ representation เพื่อให้ client/cache/proxy ทำงานร่วมกันได้
- [[OpenAPI]] — มาตรฐานคำอธิบาย HTTP API ที่เครื่องมือใช้สร้าง docs, clients และ validation

## Application Architecture

- [[State Management Concepts]] — หลักการกำหนดเจ้าของและวงจรชีวิตของ state ใน application เพื่อหลีกเลี่ยงการ sync ซ้ำซ้อน
