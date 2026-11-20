---
title: Command and API Finder
type: index
tags: [technical-knowledge, index, commands, api-reference]
status: in-progress
last_verified: 2026-11-20
---

# Command and API Finder

เริ่มจากงานที่ต้องทำ แล้วเปิดคู่มือเทคโนโลยีที่ใช้อยู่. คู่มือ API แต่ละชุดกำลังขยายทีละกลุ่ม; ใช้ concept links เป็นพื้นฐานระหว่างที่ยังไม่มี cookbook ของเทคโนโลยีนั้น.

## ต้องการทำอะไร

| งาน | เริ่มอ่าน/ใช้ | คู่มือ API |
|---|---|---|
| เขียน Python script / API | Python 3, virtual env, typing, FastAPI | [[Python Recipes]] |
| เขียน/อ่าน/แก้ข้อมูล relational database | SQL `SELECT`, `JOIN`, `INSERT`, transaction, index | [[SQL Recipes]] |
| ทำ state ที่เปลี่ยนตาม UI | Vue `ref`, React `useState`, Svelte `$state` | [[Vue API Recipes]], [[React Recipes]] |
| คำนวณค่า derived | Vue `computed`, React render-time derive | [[Vue API Recipes]], [[React Recipes]] |
| ตอบสนองการเปลี่ยนค่า / side effect | Vue `watch`, React `useEffect` | [[Vue API Recipes]], [[React Recipes]] |
| โหลดข้อมูลและยกเลิก request | `fetch` + `AbortController`, query cache | [[JavaScript Recipes]], [[React Recipes]], [[TanStack Query Cache Lifecycle]] |
| รับ/ตรวจข้อมูลภายนอก | TypeScript guard, Zod parse | [[TypeScript Recipes]], [[Zod Runtime Validation]] |
| ส่งข้อมูล parent-child | Vue props/emits/model, React props/callback | [[Vue API Recipes]], [[React Recipes]] |
| ทำ reusable logic | Vue composable, JS module/function | [[Vue API Recipes]], [[JavaScript Recipes]] |
| สร้าง HTTP API | Go `net/http`, backend framework routes | [[Go Recipes]], [[Go HTTP Handler Boundaries]] |
| จัดการ error | Go wrapping, JS try/catch | [[Go Recipes]], [[JavaScript Recipes]], [[Go Error Handling]] |
| ทำงาน async/concurrent | Promise, goroutine/channel/context | [[JavaScript Recipes]], [[Go Recipes]], [[Go Channels]], [[Go Context]] |
| เขียน test | Go table test, Vitest, Playwright | [[Go Recipes]], [[Unit Integration and End-to-End Tests]] |
| query/update database | transaction, ORM, generated SQL | [[Database Transactions]], [[Prisma Data Model and Migration Safety]], [[GORM Transactions and Associations]], [[sqlc Query Contracts and Generated Code]] |
| ทำ form และ validation | form state/resolver/schema | [[Browser Form State]], [[React Hook Form Registration and Validation]], [[VeeValidate Form and Field Lifecycle]], [[Zod Runtime Validation]] |
| deploy / operate | Dockerfile, Compose, Nginx | [[Docker Image Layers and Reproducible Builds]], [[Docker Compose Service Networking and Health]], [[Nginx Reverse Proxy Request Flow]] |

## คู่มือ API ที่มีแล้ว

- [[Zustand Recipes]] — สร้าง store, selectors, async actions, persist/test
- [[Pinia Recipes]] — setup store, `storeToRefs`, actions, subscriptions
- [[TanStack Query Recipes]] — query keys, mutations, invalidation, optimistic updates
- [[Zod Recipes]] — schema, parse/safeParse, transforms, composition
- [[TanStack Router Recipes]] — typed routes, loaders, search params, navigation
- [[TanStack Table Recipes]] — columns, render, row models, sorting/filtering
- [[TanStack Virtual Recipes]] — list/table windowing, measurement, overscan
- [[React Hook Form Recipes]] — registration, resolver, controlled widgets, field arrays
- [[VeeValidate Recipes]] — Vue form/field lifecycle, schema, dynamic fields
- [[TanStack Form Recipes]] — field state, validation, submit, async fields
- [[Tailwind CSS Recipes]] — v4 setup, utilities, themes, responsive state
- [[DaisyUI Recipes]] — plugin setup, semantic components and themes
- [[Reka UI Recipes]] — Vue primitives, dialog, controlled state, accessibility
- [[Prisma Recipes]] — schema, migrations, queries and transactions
- [[GORM Recipes]] — Go models, queries, transactions and associations
- [[sqlc Recipes]] — generate typed Go code from SQL contracts
- [[Redis Recipes]] — keys/TTL, cache-aside, structures and ops
- [[OAuth 2.0 Recipes]] — Authorization Code + PKCE, callback validation, token handling
- [[JWT Recipes]] — verification, claims, key rotation, revocation
- [[Vitest Recipes]] — test, mocks, async, coverage
- [[Playwright Recipes]] — locators, auth state, network, traces
- [[Go Testing Recipes]] — unit/table tests, HTTP handlers, race, benchmarks
- [[Docker Recipes]] — image build/run, logs, volumes, clean-up
- [[Docker Compose Recipes]] — app/db stack, health checks, profiles, exec/run
- [[Nginx Recipes]] — reverse proxy, config validation/reload, TLS and static files
- [[RabbitMQ Recipes]] — durable publish, manual ack, retry/dead-letter, confirms
- [[SvelteKit Recipes]] — route loads/actions/API endpoints/build
- [[Vite Recipes]] — scaffold, env, aliases, proxy and production build
- [[Nuxt Recipes]] — routes, SSR data, server endpoints, runtime config
- [[React Router Recipes]] — loaders/actions/fetchers/search params
- [[React with TypeScript Recipes]] — typed props/events/reducers/refs
- [[Vue with TypeScript Recipes]] — typed props/emits/composables/refs

- [[Vue API Recipes]] — `ref`, `reactive`, `computed`, `watch`, props/emits, `v-model`, lifecycle, slots, composables, directives
- [[JavaScript Recipes]] — values, arrays, async, modules, object updates, cancellation
- [[TypeScript Recipes]] — contracts, generics, unions, narrowing, `keyof`, `satisfies`
- [[React Recipes]] — components, state, effects, context, refs, optimization
- [[Go Recipes]] — modules, types, errors, HTTP, concurrency, tests
- [[Next.js Recipes]] — App Router, route params, server/client, actions, cache
- [[Python Recipes]] — Python syntax, environments, files, errors, async, FastAPI
- [[SQL Recipes]] — DDL/DML, joins, upsert, transaction และ query plan
- [[Express Recipes]] — Express routes, middleware, errors, graceful shutdown
- [[FastAPI Recipes]] — Pydantic models, dependencies, async, test
- [[Gin Recipes]] — Gin binding, route groups, middleware, handler test
- [[Fiber Recipes]] — Fiber binding, groups, error handling, testing
- [[Hono Recipes]] — Hono routes, validation, bindings, error handlers
- [[Elysia Recipes]] — Elysia schema, hooks, plugins, errors
- [[Bun Recipes]] — Bun runtime, HTTP, files, tests/build


## Backend framework recipes

[[Express Recipes]] · [[FastAPI Recipes]] · [[Gin Recipes]] · [[Fiber Recipes]] · [[Hono Recipes]] · [[Elysia Recipes]] · [[Bun Recipes]]

## UI, data and database cookbooks

[[Tailwind CSS Recipes]] · [[DaisyUI Recipes]] · [[Reka UI Recipes]] · [[Prisma Recipes]] · [[GORM Recipes]] · [[sqlc Recipes]] · [[Redis Recipes]]

## Security and testing recipes

[[OAuth 2.0 Recipes]] · [[JWT Recipes]] · [[Vitest Recipes]] · [[Playwright Recipes]] · [[Go Testing Recipes]]

## Frontend framework and infrastructure recipes

[[React with TypeScript Recipes]] · [[Vue with TypeScript Recipes]] · [[SvelteKit Recipes]] · [[Vite Recipes]] · [[Nuxt Recipes]] · [[React Router Recipes]] · [[Docker Recipes]] · [[Docker Compose Recipes]] · [[Nginx Recipes]] · [[RabbitMQ Recipes]]

## เทคโนโลยีทั้งหมด

ทุกภาษาหลักใน vault มีสูตรใช้งานเริ่มต้น: [[JavaScript Recipes]], [[TypeScript Recipes]], [[Go Recipes]], [[Python Recipes]], [[SQL Recipes]]. ดู [[Technology-Index]] เพื่อเปิด overview ทุกตัว. เป้าหมายของสารบัญนี้คือเพิ่ม cookbook สำหรับเทคโนโลยีที่เหลือตามลำดับการใช้งาน; จนกว่าจะเติม ให้ใช้ concept index และ official docs ที่ผูกกับแต่ละ overview.
