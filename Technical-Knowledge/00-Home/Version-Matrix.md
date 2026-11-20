---
title: Version and Update Tracker
type: reference
tags: [technical-knowledge, versions, maintenance]
status: published
last_verified: 2026-11-20
sources:
  - Technical-Knowledge/00-Home/Recent-Updates.md
  - Technical-Knowledge/13-References/Reference-Catalog.md
---

# Version & Update Tracker

เอกสารหลักของคลังนี้เป็นเนื้อหา Markdown ในเครื่อง ส่วนตารางนี้จด **การเปลี่ยนแปลงสำคัญที่ค้นพบจากแหล่งทางการ** ณ 2026-11-20 เพื่อให้เนื้อหา offline มีบริบทปัจจุบัน ไม่ใช่ตัวแทน changelog ทั้งหมด และไม่ควรใช้แทนการตรวจ patch/security release ก่อน deploy

> [!important] อ่านเวอร์ชันอย่างปลอดภัย
> แยก stable, maintenance, alpha, beta และ experimental ให้ชัด ตรวจ runtime/plugin compatibility และ migration guide ทุกครั้งที่อัปเกรด major. เวอร์ชันที่ระบุคือ snapshot ล่าสุดที่แหล่งทางการแสดงตอนค้น ไม่ใช่คำสั่งให้ใช้เลขนั้นกับทุกโปรเจกต์

## Update snapshots

| เทคโนโลยี | สถานะ/การเปลี่ยนแปลงที่ยืนยันจากแหล่งทางการ | ความหมายต่อการเรียนรู้ |
|---|---|---|
| React | 19.3 stable: View Transitions และ Fragment Refs เสถียร; เพิ่มการทำงานกับ Context จาก Server Components และปรับ transition/effect behavior | เรียน transition กับ server/client boundary จาก docs รุ่นล่าสุด; ทดสอบ hydration/Strict Mode |
| Next.js | 16.4 (6 Oct): lazy compilation, Turbopack output เล็กลง, React 19.3 features และ Cache Components improvements | คู่มือ Next 16 ควรยึด App Router/cache model; อย่าคัด config เก่าจาก v13/v14 |
| React Router | 8.5.2 (18 Nov): fixes route/action metadata, streamed Suspense, HEAD stream resource handling; v8.5 deprecates router view-transition API in favor of React 19.3 `<ViewTransition>` | แก้ migration note และตรวจ behavior เมื่อ action throw / HEAD stream |
| Vue | Vue 3 เป็น major ปัจจุบัน; ใช้ release page ตรวจ minor/patch และแยก stable จาก prerelease | TypeScript definition compatibility อาจเปลี่ยนตาม minor; pin minor สำหรับ library compatibility |
| Nuxt | Active major คือ Nuxt 4; หน้า deploy แสดง Nuxt 4.6.4; Nuxt 3 สิ้นสุด maintenance 31 Jul 2026 ตาม roadmap ที่ตรวจ | คู่มือใหม่ใช้ Nuxt 4 conventions; migration จาก Nuxt 3 ต้องตรวจ breaking changes |
| SvelteKit | SvelteKit 3 stable 1 Oct 2026; `sv` 1.0 และ migration command `npx sv migrate sveltekit-3` | ตรวจ migration guide โดยเฉพาะ config, adapters และ API ที่เปลี่ยน |
| Vite | Vite 8.3 เป็น current release train ที่หน้า releases แสดง; Vite 8 รวม Rolldown เป็น bundler หลัก | ตรวจ plugin ecosystem และ migration; Vite 8 ต้องการ Node 20.19+ หรือ 22.12+ |
| Go | Go 1.27.4 (10 Nov) เป็น patch ล่าสุดที่ตรวจ; Go 1.27 เพิ่ม generic methods, `encoding/json/v2` และปรับ TLS/standard library | ตรวจ Go release page และ security releases ของ branch ที่ deploy; อย่าอ้าง Go 1.26 เป็นรุ่นล่าสุดโดยไม่ตรวจ |
| Bun | Bun 1.4.4 เป็นรุ่นล่าสุดที่ตรวจ; 1.4 เพิ่ม HTTP/2 ใน `Bun.serve`, 1.4.4 แก้ regression ของ compile cache | runtime compatibility ยังต้องเช็ค library, native module, TLS และ deployment target |
| TanStack Table | v9 stable ตั้งแต่ Aug 2026: tree-shakable feature plugins, TanStack Store-based state/fine-grained reactivity และ adapter เพิ่มขึ้น | v8 guide เก่าใช้ API คนละรุ่น; อ่าน migration guide ก่อนย้าย |
| TanStack Form | v2 เป็น alpha ตามประกาศ Aug 2026; ปรับ validators/API จาก v1 | ใช้ v1 stable สำหรับ production เว้นแต่ยอมรับ prerelease risk และ pin alpha โดยตั้งใจ |
| Prisma | Prisma ORM 8 ยังเป็น release candidate ณ หน้า status ที่ตรวจ; CLI และ database libraries ออกคนละ version; Prisma 7 ยังคงมี support | ตรวจ `prisma.config.ts`, client package/config และ migration guide ตาม major |
| Tailwind CSS | v4.3 (May 2026): scrollbar utilities, logical properties, colors; v4 มี CSS-first config และ browser requirements ใหม่ | v3 กับ v4 syntax/config ไม่ควรผสม; เบราว์เซอร์เก่ากว่า baseline อาจต้องอยู่ v3.4 |
| Vitest | 5.1 เป็น release train ปัจจุบัน; ต้องใช้ Vite >=6.4 และ Node >=22.12 ตาม migration guide | ตรวจ peer dependencies; Vitest major ไม่ได้ตาม Vite major แบบเลขเดียวกัน |
| Playwright | Release notes ปัจจุบันถึง 1.65: test runner บน Bun, failures-only reporting; Node 20 ไม่อยู่ใน CI support แล้ว (ใช้ 22/24/26) | lock browser binaries ตาม Playwright version และอ่าน breaking changes ก่อนอัปเดต |
| OAuth 2.0 | RFC 9700 คือ OAuth 2.0 Security BCP ที่ควรอ่านควบคู่ RFC 6749 | authorization code + PKCE และการลด insecure legacy flow เป็นประเด็นหลัก |

## รายการเทคโนโลยีทั้งหมด

ทุก overview มีคำอธิบายและแหล่งอ้างอิงเฉพาะรายการ ใช้ตารางนี้เปิดดูเป็นกลุ่ม:

- [[Technology-Index]] — 45 technologies และ overview
- [[Recent-Updates]] — สรุปการเปลี่ยนแปลงล่าสุดที่บันทึกเป็นเนื้อหา offline
- [[Technology-Selection-Guide]] — เลือก technology ตามโจทย์

## Workflow ดูแลข้อมูล offline

1. อ่าน release notes, security advisories และ migration guide ของ dependency ที่โปรเจกต์ใช้อยู่จริง
2. สรุปการเปลี่ยนแปลงที่กระทบความรู้ใน `Recent-Updates.md` และปรับ concept note แบบ local ไม่ฝากสาระสำคัญไว้ในลิงก์เว็บอย่างเดียว
3. แก้ตัวอย่าง/API ให้ระบุ major/minor และ runtime; เพิ่ม `last_verified` หลังตรวจจริง
4. ระบุความไม่แน่ใจหรือ prerelease ให้ชัด ห้ามทำให้ลิงก์ที่ยังไม่ได้อ่านดูเหมือนเนื้อหายืนยันแล้ว

แหล่งอ้างอิงรายเทคโนโลยีและ release notes อยู่ใน [[Reference-Catalog]] และ [[Recent-Updates]]; ใช้หน้าทางการของแต่ละรายการเป็นหลักฐานสำหรับ snapshot ไม่ใช้ตารางนี้แทน changelog.



## แหล่งอ้างอิงของ snapshots

- [https://github.com/pmndrs/zustand/releases](https://github.com/pmndrs/zustand/releases)
- [https://github.com/vuejs/pinia/releases](https://github.com/vuejs/pinia/releases)
- [https://github.com/colinhacks/zod/releases](https://github.com/colinhacks/zod/releases)
- [https://github.com/honojs/hono/releases](https://github.com/honojs/hono/releases)
- [https://github.com/expressjs/express/releases](https://github.com/expressjs/express/releases)
- [https://github.com/gofiber/fiber/releases](https://github.com/gofiber/fiber/releases)
- [https://github.com/gin-gonic/gin/releases](https://github.com/gin-gonic/gin/releases)
- [https://fastapi.tiangolo.com/release-notes/](https://fastapi.tiangolo.com/release-notes/)
- [https://github.com/redis/redis/releases](https://github.com/redis/redis/releases)
- [https://github.com/docker/compose/releases](https://github.com/docker/compose/releases)
- [https://www.rabbitmq.com/release-information](https://www.rabbitmq.com/release-information)
- [https://nuxt.com/docs/4.x/community/roadmap/](https://nuxt.com/docs/4.x/community/roadmap/)
- [https://react.dev/blog/2026/09/09/react-19-3](https://react.dev/blog/2026/09/09/react-19-3)
- [https://nextjs.org/blog/next-16-4](https://nextjs.org/blog/next-16-4)
- [https://reactrouter.com/changelog](https://reactrouter.com/changelog)
- [https://nuxt.com/deploy](https://nuxt.com/deploy)
- [https://svelte.dev/blog/sveltekit-3-is-here](https://svelte.dev/blog/sveltekit-3-is-here)
- [https://vite.dev/blog/announcing-vite8](https://vite.dev/blog/announcing-vite8)
- [https://vite.dev/releases](https://vite.dev/releases)
- [https://go.dev/doc/go1.27](https://go.dev/doc/go1.27)
- [https://go.dev/doc/devel/release](https://go.dev/doc/devel/release)
- [https://go.dev/dl/](https://go.dev/dl/)
- [https://bun.sh/blog/bun-v1.4](https://bun.sh/blog/bun-v1.4)
- [https://bun.sh/blog/bun-v1.4.4](https://bun.sh/blog/bun-v1.4.4)
- [https://tanstack.com/blog/announcing-tanstack-table-v9](https://tanstack.com/blog/announcing-tanstack-table-v9)
- [https://tanstack.com/blog/announcing-tanstack-form-v2-alpha](https://tanstack.com/blog/announcing-tanstack-form-v2-alpha)
- [https://www.prisma.io/docs/orm/release-status](https://www.prisma.io/docs/orm/release-status)
- [https://www.prisma.io/docs/orm/supported-databases](https://www.prisma.io/docs/orm/supported-databases)
- [https://www.prisma.io/changelog](https://www.prisma.io/changelog)
- [https://tailwindcss.com/blog/tailwindcss-v4-3](https://tailwindcss.com/blog/tailwindcss-v4-3)
- [https://vitest.dev/releases.html](https://vitest.dev/releases.html)
- [https://vitest.dev/guide/migration/](https://vitest.dev/guide/migration/)
- [https://playwright.dev/docs/release-notes](https://playwright.dev/docs/release-notes)
- [https://www.rfc-editor.org/rfc/rfc9700](https://www.rfc-editor.org/rfc/rfc9700)

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
