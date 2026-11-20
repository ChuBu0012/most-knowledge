---
title: Recent Technology Updates
type: reference
tags: [technical-knowledge, release-notes, updates]
status: published
last_verified: 2026-11-20
---

# Recent Technology Updates

สรุปนี้เก็บการเปลี่ยนแปลงที่ส่งผลต่อการเรียนรู้/การย้ายระบบไว้ใน Vault เพื่ออ่านได้ offline. วันอ้างอิงคือ **2026-11-20**. เป็น curated highlights ไม่ใช่รายการทุก patch; ดู [[Version-Matrix]] และหน้าของแต่ละ technology เพื่อรู้ขอบเขต/ลิงก์ทางการ

## Frontend frameworks and tools

### React 19.3

React 19.3 ทำให้ `<ViewTransition>` และ Fragment Refs เป็น stable APIs. `<ViewTransition>` ใช้จัด animation ของ element ที่ enter, exit, move หรือ update โดย React ผูก transition กับ update ที่ทำผ่าน transition mechanism; update เร่งด่วนไม่ได้ animate โดยอัตโนมัติ. React 19.3 ยังให้ Server Components render Context ที่ import จาก Client module ได้โดยตรง ลด wrapper provider ที่มีหน้าที่แค่ส่งค่า. Strict Mode เพิ่มการตรวจ effect ระหว่าง hydration ให้ใกล้กับ client root. อย่าลืมว่าความสามารถ Server Components/Server Functions ต้องอาศัย framework/runtime ที่รองรับและต้องตรวจ authorization ที่ server boundary.

อ่านต่อ: [[React Rendering Model]] · [[React Effect Synchronization]] · [[React Server and Client Components]]

### Next.js 16.4

Next.js 16.4 (6 Oct 2026) เน้น lazy compilation, ลด Turbopack output, รองรับ React 19.3 และปรับ Cache Components. การคิดเรื่อง cache ควรแยก request memoization, data cache, route/render cache และ browser/router cache; อย่าถือว่า “server rendered” แปลว่า fresh ทุก request. Cache key และ invalidation เป็นส่วนของความถูกต้องและความปลอดภัย โดยเฉพาะข้อมูลที่ขึ้นกับผู้ใช้. ตรวจคำแนะนำรุ่น 16 และ security updates ก่อน deploy.

อ่านต่อ: [[Next.js with TypeScript]] · [[React Server and Client Components]] · [[TanStack Query Cache Lifecycle]]

### React Router 8.5.2

รุ่น 8.5.2 (18 Nov 2026) แก้ metadata หลัง action ล้มเหลว, streaming Suspense/hydration และการปล่อย resource หลัง HEAD request. ใน 8.5 API view-transition ของ Router ถูก deprecate เพื่อไปใช้ React `<ViewTransition>` เมื่อใช้ React 19.3 ขึ้นไป. แยก navigation state, loader data และ action submission ใน UI; ระวัง streaming response ต้อง cancel/cleanup เมื่อ client เลิกอ่าน.

อ่านต่อ: [[React Router Framework]] · [[HTTP Semantics and REST]]

### Vue 3

Vue 3 ยังคงเป็น major ปัจจุบันจากหน้า releases ที่ตรวจ. ใช้ stable release และ migration guide; alpha/beta/RC มีไว้ทดสอบและไม่ควรปะปนกับคู่มือ production. TypeScript definitions อาจเปลี่ยนความเข้ากันได้ระหว่าง minor releases เมื่อรองรับ TypeScript รุ่นใหม่ขึ้น. ออกแบบ composables และ libraries ให้ระบุ peer dependency/minimum Vue minor ที่ต้องการ.

อ่านต่อ: [[Vue Reactivity and Computed State]] · [[Vue Composables]]

### Nuxt 4

Nuxt 4 เป็น active major; เอกสาร deployment แสดง 4.6.4. Nuxt 3 สิ้นสุด support วันที่ 31 Jul 2026 ตาม roadmap ที่ตรวจ. Nuxt 4.6 เพิ่ม/ขยาย server APIs ที่ Nuxt Auth Utils รุ่นใหม่ใช้งาน จึงควรตรวจคู่เวอร์ชัน module/runtime และอ่าน migration guide จาก Nuxt 3. อย่ายึด docs v3 โดยไม่ระบุว่าเป็น legacy.

อ่านต่อ: [[Nuxt]] · [[Nitro]] · [[Session-Management]]

### SvelteKit 3 และ `sv` 1.0

SvelteKit 3 stable วันที่ 1 Oct 2026; `sv` CLI ถึง 1.0 และมี `sv migrate sveltekit-3` เพื่อทำ migration ที่อัตโนมัติได้พร้อม TODO สำหรับส่วนที่ต้องแก้เอง. Major release ยังคง model เดิมแต่ปรับ type safety และ cleanup API; ตรวจ migration guide แทนการคาดเดาว่า config เดิมใช้ได้ทั้งหมด.

อ่านต่อ: [[SvelteKit]] · [[Svelte Runes and Reactivity]]

### Vite 8

Vite 8 เปลี่ยน bundler หลักเป็น Rolldown ซึ่งรวมบทบาท dev/build bundlers เดิมไว้ใน Rust-based bundler; Vite 8.3 เป็น release train ปัจจุบันจากหน้า releases ที่ตรวจ. Vite 8 รองรับ Node 20.19+ หรือ 22.12+. Plugin migration และ behavior ที่อาศัย Rollup/esbuild internals ต้องทดสอบ; built-in `resolve.tsconfigPaths` ยัง opt-in และมีต้นทุน performance.

อ่านต่อ: [[Vite Development and Production Builds]] · [[Vite]] · [[Vitest]]

## Backend and data

### Go toolchain

Go 1.27.4 (10 Nov 2026) เป็น patch ล่าสุดที่ตรวจ. Go 1.27 เพิ่ม generic methods, ยอมให้ generic function inference ทำงานใน assignment contexts เพิ่ม `encoding/json/v2` และ `jsontext`, UUID package และการเปลี่ยนแปลง TLS/HTTP. Go 1.27 ต้องใช้ macOS 13 Ventura หรือใหม่กว่า. การย้าย `encoding/json` อาจมีผลต่อ duplicate object names/invalid UTF-8 semantics; อ่าน compatibility notes ก่อนเปลี่ยน. Go 1.26 เพิ่ม Green Tea GC และ `go fix` modernizers; benchmark workload จริงก่อนสรุปผล runtime.

อ่านต่อ: [[Go]] · [[Go Goroutines]] · [[Go Context]] · [[Go Testing]]

### Bun 1.4.4

Bun 1.4.4 เป็น patch ล่าสุดที่ตรวจ. สาย 1.4 เพิ่ม HTTP/2 ให้ `Bun.serve`; รุ่น 1.4.4 แก้ regression เรื่อง compile cache exit time จาก 1.4.3. ก่อนนำไป production ให้ทดสอบ protocol, TLS, library compatibility และ graceful shutdown ใน environment จริง.

อ่านต่อ: [[Bun]] · [[Hono]] · [[Elysia]]

### TanStack Table v9 stable

v9 stable วันที่ 4 Aug 2026 ปรับ architecture ให้ tree-shakable feature plugins และใช้ TanStack Store เป็นแกน state ทำ fine-grained reactivity กับ adapters หลาย framework. Headless model ยังคงอยู่ แต่ API/adapter setup เปลี่ยนจาก v8; migration guide แยกตาม framework. เริ่มจาก row model ที่ต้องใช้จริงเพื่อลด bundle และทดสอบ custom feature/plugin.

อ่านต่อ: [[TanStack-Table]] · [[TanStack-Virtual]] · [[TanStack Query Cache Lifecycle]]

### TanStack Form v2 alpha

Form v2 เปิด alpha 6 Aug 2026. เป้าหมายคือปรับ validator model ให้ยืดหยุ่นขึ้น, type safety และ runtime performance. API alpha อาจเปลี่ยน; stable v1 เป็นตัวเลือก production ที่ความเสี่ยงต่ำกว่า. ห้ามใช้ snippet v2 โดยไม่ปัก prerelease และแยกจาก v1 docs.

อ่านต่อ: [[TanStack-Form]] · [[Browser Form State]] · [[Zod Runtime Validation]]

### Prisma ORM 8 release candidate

ณ 20 Nov 2026 Prisma ORM 8 ยังเป็น release candidate และ package `latest` เป็น RC; อย่าถือว่าเป็น GA. CLI และ database libraries version ไม่ตรงกันและแยก package. รุ่น 8 เปลี่ยนจาก generated client ไป contract model, query API ใหม่ และ migration workflow; บาง database adapters ยัง early access/experimental. Prisma 7 ยังคงเอกสารและ support แยกต่างหาก. ตรวจ runtime floor, feature gaps, migration guide, สำรองฐานข้อมูล และ pin major ก่อนเริ่ม migration.

อ่านต่อ: [[Prisma]] · [[Database-Transactions]] · [[SQL Indexes and Query Plans]]

## UI and testing

### Tailwind CSS 4.3

Tailwind 4.3 (8 May 2026) เพิ่ม scrollbar utilities, logical-property utilities และสีใหม่; v4 เปลี่ยนสู่ CSS-first configuration และใช้ CSS features สมัยใหม่. Baseline browser คือ Safari 16.4+, Chrome 111+, Firefox 128+. หากต้องรองรับ browser เก่ากว่านี้ คู่มือทางการแนะนำอยู่ Tailwind 3.4. Upgrade tool ช่วยย้ายได้ แต่ต้อง review diff และตรวจ design/production build.

อ่านต่อ: [[Tailwind CSS]] · [[DaisyUI]] · [[Reka UI]]

### Vitest 5.1

Vitest 5.1 เป็น release train ปัจจุบันตามหน้า releases; ต้องใช้ Vite >=6.4 และ Node >=22.12. ใน v5 `clearMocks` เปิดเป็นค่าเริ่มต้น และ Vite เป็น peer dependency ที่ควรประกาศชัด (โดยเฉพาะ Yarn). ตรวจการพึ่งพา mocks, setup files, browser mode และ plugin compatibility ตอนอัปเกรด.

อ่านต่อ: [[Vitest]] · [[Vite Development and Production Builds]]

### Playwright 1.65

Release notes ปัจจุบันถึง 1.65; test runner ทำงานบน Bun ผ่าน `bun --bun playwright test` พร้อม caveats เรื่อง watch mode, TypeScript config และ traces. มี failures-only reporter และ breaking changes ด้าน TS class fields, inert elements, cookie matching และ proxy credentials. รุ่นนี้ไม่ทดสอบ Node 20 แล้ว; ใช้ Node 22/24/26 ตาม support notes. Pin Playwright package และ browser binaries เป็นชุดเดียวกัน.

อ่านต่อ: [[Playwright]] · [[React Effect Synchronization]] · [[HTTP-Authentication]]

## Security baseline

### OAuth 2.0

RFC 9700 ยังคือ Security Best Current Practice สำหรับ OAuth 2.0. Authorization Code + PKCE เป็นแนวทางหลักสำหรับ public clients; หลีกเลี่ยง implicit grant และ resource-owner password credentials. Redirect URI ต้อง exact match, ป้องกัน CSRF/mix-up, ตรวจ issuer/audience และเก็บ client secret เฉพาะ confidential client ฝั่ง server.

อ่านต่อ: [[OAuth-2.0]] · [[JWT]] · [[Session-Management]]

## ความครอบคลุมและช่องว่าง

รายการทั้งหมดที่อยู่ใน scope มีหน้า overview และ official docs/release links ใน [[Technology-Index]]. การเขียนรายละเอียดทุก release note และทุก API ยังเป็นงานต่อเนื่อง; ประเด็นในหน้านี้เป็นเรื่องที่ค้นคว้าและสรุปไว้ในเครื่องจริง ไม่ได้อ้างว่าเป็น archive เต็มของแต่ละ upstream project.


### Zustand 5.1, Pinia 4.1 และ Zod 4.6

Zustand 5.1 (6 Nov) ทำให้ `persist` รองรับ PromiseLike storage/migration และ `rehydrate()` await ได้; SSR/hydration ต้องรอให้ state โหลดครบ. Pinia 4.1 (14 Oct) เพิ่ม `getStores()` และเตือน store ที่ถูกแทนที่; v4 เป็น ESM-only. Zod 4.6 เพิ่ม `.validate()`, JSON Schema improvements และ `z.withParser()`; ตรวจ resolver ecosystem และ migration จาก Zod 3.

อ่านต่อ: [[Zustand]] · [[Pinia]] · [[Zod]] · [[Zod Runtime Validation]]

### Hono, Express, Fiber, Gin และ FastAPI

- **Hono 4.13.19** (16 Nov): 4.13.18 ปิดปัญหา security ใน `validator()`, `bodyLimit()`, mount path และ double decoding ของ static path; หากใช้ส่วนดังกล่าวให้อัปเดตและทบทวน config.
- **Express 5.3.0** (9 Oct): `res.send()` แก้การส่ง `Content-Length` พร้อม `Transfer-Encoding` ที่ขัด HTTP semantics.
- **Fiber 3.7.0** (9 Nov): อัปเดต fasthttp 1.78 และ map query/form binding; Fiber 3.6 กำหนด Go 1.26+.
- **Gin 1.12.0**: binding รองรับ `encoding.TextUnmarshaler` เพิ่ม error retrieval helpers.
- **FastAPI 0.163.1** (15 Nov): 0.163 เพิ่ม concurrency limits ใน dependencies; 0.162.6 ยกเลิก Python 3.10 support.

อ่านต่อ: [[Hono]] · [[Express]] · [[Fiber]] · [[Gin]] · [[FastAPI]] · [[HTTP Request Lifecycle]]

### Redis, Compose และ RabbitMQ

Redis 8.10.3 เป็น latest tag ที่ตรวจ; รุ่น 8.10.2 มี security fixes สำหรับ transaction ACL และ cluster bus authentication. Docker Compose 5.7.1 ปรับ `Up` ให้ Create/Start ใช้ daemon snapshot เดียวและแก้ reconciliation ของ images ใน releases ก่อนหน้า; ตรวจ behavior เมื่ออัปเกรด. RabbitMQ 4.4.1 (16 Nov) เพิ่ม quorum queue delayed/deferred messages, Erlang 29, post-quantum TLS และ native STOMP. ตรวจ client protocol support และ release support lifecycle ก่อนเลือก broker version.

อ่านต่อ: [[Redis]] · [[Docker-Compose]] · [[RabbitMQ]] · [[Redis Cache-Aside]] · [[RabbitMQ Acknowledgements and Redelivery]]

### TanStack Table v9 และ Form v2

TanStack Table v9 stable และ Form v2 alpha เป็นคนละสถานะ: Table v9 เป็น stable major ที่ต้อง migration จาก v8; Form v2 ยังทดลองได้แต่ไม่ควรแทน stable v1 ใน production โดยไม่ยอมรับความเสี่ยง. Adapter และ API เปลี่ยนราย framework; อย่าคัดลอกตัวอย่างต่าง major มาปนกัน.

### Nuxt และ Vue

Nuxt 4 เป็น active major และ Nuxt 3 สิ้นสุด maintenance 31 Jul 2026 ตาม roadmap; Vue releases ไม่มีรอบตายตัวและแยก prerelease จาก stable. ตรวจ module compatibility กับ Nuxt/Vue minor ที่ pin ในโปรเจกต์ โดยเฉพาะ auth/server modules.

### Sources for additional snapshots

- Zustand: https://github.com/pmndrs/zustand/releases
- Pinia: https://github.com/vuejs/pinia/releases
- Zod: https://github.com/colinhacks/zod/releases
- Hono: https://github.com/honojs/hono/releases
- Express: https://github.com/expressjs/express/releases
- Fiber: https://github.com/gofiber/fiber/releases
- Gin: https://github.com/gin-gonic/gin/releases
- FastAPI: https://fastapi.tiangolo.com/release-notes/
- Redis: https://github.com/redis/redis/releases
- Docker Compose: https://github.com/docker/compose/releases
- RabbitMQ: https://www.rabbitmq.com/release-information
- Nuxt: https://nuxt.com/docs/4.x/community/roadmap/

## แหล่งอ้างอิงทางการของ snapshots

- React 19.3: https://react.dev/blog/2026/09/09/react-19-3
- Next.js 16.4: https://nextjs.org/blog/next-16-4
- React Router 8.5.2: https://reactrouter.com/changelog
- Nuxt releases/support: https://nuxt.com/docs/4.x/community/roadmap/ · https://nuxt.com/deploy
- SvelteKit 3: https://svelte.dev/blog/sveltekit-3-is-here
- Vite 8/release support: https://vite.dev/blog/announcing-vite8 · https://vite.dev/releases
- Go 1.27: https://go.dev/doc/go1.27 · https://go.dev/doc/devel/release · https://go.dev/dl/
- Bun 1.4: https://bun.sh/blog/bun-v1.4 · https://bun.sh/blog/bun-v1.4.4
- TanStack Table v9: https://tanstack.com/blog/announcing-tanstack-table-v9
- TanStack Form v2 alpha: https://tanstack.com/blog/announcing-tanstack-form-v2-alpha
- Prisma ORM 8 status: https://www.prisma.io/docs/orm/release-status · https://www.prisma.io/docs/orm/supported-databases · https://www.prisma.io/changelog
- Tailwind CSS 4.3: https://tailwindcss.com/blog/tailwindcss-v4-3
- Vitest 5: https://vitest.dev/releases.html · https://vitest.dev/guide/migration/
- Playwright 1.65: https://playwright.dev/docs/release-notes
- OAuth 2.0 Security BCP: https://www.rfc-editor.org/rfc/rfc9700

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
