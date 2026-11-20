---
title: Reference Catalog
type: index
tags: [technical-knowledge, references, sources]
status: published
last_verified: 2026-11-20
---

# Reference Catalog

รวมแหล่งอ้างอิงที่ผูกกับทุก knowledge unit ในคลัง แยกตามหัวข้อและประเภทแหล่งข้อมูล เพื่อให้เปิดคู่มือทางการ, API reference, standard และ release notes ได้ตรงจุด. ตัวเนื้อหาในแต่ละโน้ตยังมี references ที่เกี่ยวข้องเฉพาะเรื่อง.

## วิธีใช้

- เริ่มจาก technology/concept ที่กำลังศึกษา แล้วเปิดแหล่งประเภท API/reference สำหรับ syntax, guide สำหรับ workflow, และ release/migration notes สำหรับอัปเกรด.
- สำหรับ security และ protocol ให้ยึด RFC/specification เป็นหลัก; blog ใช้ดูบริบทและประกาศเท่านั้น.
- ลิงก์ภายนอกต้องตรวจ version และวันที่ก่อนใช้กับ production; catalog เป็นดัชนี ไม่ใช่คำรับรองว่า source ทุกฉบับยังเป็น latest.

**Coverage:** 170 technology/concept notes.

## Topics

### 00-Home

- [[Technical-Knowledge/00-Home/Recent-Updates|Recent Technology Updates]]
  - **Release notes and updates:** [source 1](https://github.com/pmndrs/zustand/releases) · [source 2](https://github.com/vuejs/pinia/releases) · [source 3](https://github.com/colinhacks/zod/releases) · [source 4](https://github.com/honojs/hono/releases) · [source 5](https://github.com/expressjs/express/releases) · [source 6](https://github.com/gofiber/fiber/releases) · [source 7](https://github.com/gin-gonic/gin/releases) · [source 8](https://fastapi.tiangolo.com/release-notes/) · [source 9](https://github.com/redis/redis/releases) · [source 10](https://github.com/docker/compose/releases) · [source 11](https://www.rabbitmq.com/release-information) · [source 12](https://react.dev/blog/2026/09/09/react-19-3) · [source 13](https://nextjs.org/blog/next-16-4) · [source 14](https://reactrouter.com/changelog) · [source 15](https://svelte.dev/blog/sveltekit-3-is-here) · [source 16](https://vite.dev/blog/announcing-vite8) · [source 17](https://vite.dev/releases) · [source 18](https://go.dev/doc/devel/release) · [source 19](https://bun.sh/blog/bun-v1.4) · [source 20](https://bun.sh/blog/bun-v1.4.4) · [source 21](https://tanstack.com/blog/announcing-tanstack-table-v9) · [source 22](https://tanstack.com/blog/announcing-tanstack-form-v2-alpha) · [source 23](https://www.prisma.io/docs/orm/release-status) · [source 24](https://www.prisma.io/changelog) · [source 25](https://tailwindcss.com/blog/tailwindcss-v4-3) · [source 26](https://vitest.dev/releases.html) · [source 27](https://playwright.dev/docs/release-notes)
  - **Official guides and documentation:** [source 1](https://nuxt.com/docs/4.x/community/roadmap/) · [source 2](https://nuxt.com/deploy) · [source 3](https://go.dev/doc/go1.27) · [source 4](https://go.dev/dl/) · [source 5](https://www.prisma.io/docs/orm/supported-databases) · [source 6](https://vitest.dev/guide/migration/)
  - **Standards and specifications:** [source 1](https://www.rfc-editor.org/rfc/rfc9700)
- [[Technical-Knowledge/00-Home/Glossary|Technical Glossary]]
  - **Official guides and documentation:** [source 1](https://developer.mozilla.org/en-US/docs/Glossary)
  - **Standards and specifications:** [source 1](https://www.rfc-editor.org/rfc/rfc6749) · [source 2](https://www.rfc-editor.org/rfc/rfc7519)
- [[Technical-Knowledge/00-Home/Version-Matrix|Version and Update Tracker]]
  - **Release notes and updates:** [source 1](https://github.com/pmndrs/zustand/releases) · [source 2](https://github.com/vuejs/pinia/releases) · [source 3](https://github.com/colinhacks/zod/releases) · [source 4](https://github.com/honojs/hono/releases) · [source 5](https://github.com/expressjs/express/releases) · [source 6](https://github.com/gofiber/fiber/releases) · [source 7](https://github.com/gin-gonic/gin/releases) · [source 8](https://fastapi.tiangolo.com/release-notes/) · [source 9](https://github.com/redis/redis/releases) · [source 10](https://github.com/docker/compose/releases) · [source 11](https://www.rabbitmq.com/release-information) · [source 12](https://react.dev/blog/2026/09/09/react-19-3) · [source 13](https://nextjs.org/blog/next-16-4) · [source 14](https://reactrouter.com/changelog) · [source 15](https://svelte.dev/blog/sveltekit-3-is-here) · [source 16](https://vite.dev/blog/announcing-vite8) · [source 17](https://vite.dev/releases) · [source 18](https://go.dev/doc/devel/release) · [source 19](https://bun.sh/blog/bun-v1.4) · [source 20](https://bun.sh/blog/bun-v1.4.4) · [source 21](https://tanstack.com/blog/announcing-tanstack-table-v9) · [source 22](https://tanstack.com/blog/announcing-tanstack-form-v2-alpha) · [source 23](https://www.prisma.io/docs/orm/release-status) · [source 24](https://www.prisma.io/changelog) · [source 25](https://tailwindcss.com/blog/tailwindcss-v4-3) · [source 26](https://vitest.dev/releases.html) · [source 27](https://playwright.dev/docs/release-notes)
  - **Official guides and documentation:** [source 1](https://nuxt.com/docs/4.x/community/roadmap/) · [source 2](https://nuxt.com/deploy) · [source 3](https://go.dev/doc/go1.27) · [source 4](https://go.dev/dl/) · [source 5](https://www.prisma.io/docs/orm/supported-databases) · [source 6](https://vitest.dev/guide/migration/)
  - **Standards and specifications:** [source 1](https://www.rfc-editor.org/rfc/rfc9700)

### 01-Fundamentals/HTTP

- [[Technical-Knowledge/01-Fundamentals/HTTP/HTTP|HTTP]]
  - **Official guides and documentation:** [source 1](https://developer.mozilla.org/en-US/docs/Web/HTTP)
- [[Technical-Knowledge/01-Fundamentals/HTTP/HTTP-Request-Lifecycle|HTTP Request Lifecycle]]
  - **Official guides and documentation:** [source 1](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)

### 01-Fundamentals/Programming

- [[Technical-Knowledge/01-Fundamentals/Programming/JavaScript|JavaScript]]
  - **Official guides and documentation:** [source 1](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
  - **Standards and specifications:** [source 1](https://tc39.es/ecma262/)
- [[Technical-Knowledge/01-Fundamentals/Programming/JavaScript-Closures|JavaScript Closures]]
  - **Official guides and documentation:** [source 1](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)
- [[Technical-Knowledge/01-Fundamentals/Programming/JavaScript-Error-Handling|JavaScript Error Handling]]
  - **Official guides and documentation:** [source 1](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Control_flow_and_error_handling)
- [[Technical-Knowledge/01-Fundamentals/Programming/JavaScript-Execution-Model|JavaScript Execution Model]]
  - **Official guides and documentation:** [source 1](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Event_loop)
- [[Technical-Knowledge/01-Fundamentals/Programming/JavaScript-Modules|JavaScript Modules]]
  - **Official guides and documentation:** [source 1](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)
- [[Technical-Knowledge/01-Fundamentals/Programming/JavaScript-Promises|JavaScript Promises]]
  - **Official guides and documentation:** [source 1](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)

### 01-Fundamentals/SQL

- [[Technical-Knowledge/01-Fundamentals/SQL/Database-Transactions|Database Transactions]]
  - **Official guides and documentation:** [source 1](https://www.postgresql.org/docs/current/tutorial-transactions.html) · [source 2](https://www.postgresql.org/docs/current/transaction-iso.html)
- [[Technical-Knowledge/01-Fundamentals/SQL/SQL|SQL]]
  - **Official guides and documentation:** [source 1](https://www.postgresql.org/docs/current/)
- [[Technical-Knowledge/01-Fundamentals/SQL/SQL-Indexes-and-Query-Plans|SQL Indexes and Query Plans]]
  - **Official guides and documentation:** [source 1](https://www.postgresql.org/docs/current/using-explain.html)

### 01-Fundamentals/Type-System

- [[Technical-Knowledge/01-Fundamentals/Type-System/TypeScript|TypeScript]]
  - **Official guides and documentation:** [source 1](https://www.typescriptlang.org/docs/) · [source 2](https://devblogs.microsoft.com/typescript/)
  - **Release notes and updates:** [source 1](https://www.typescriptlang.org/docs/handbook/release-notes/)
- [[Technical-Knowledge/01-Fundamentals/Type-System/TypeScript-Generics|TypeScript Generics]]
  - **Official guides and documentation:** [source 1](https://www.typescriptlang.org/docs/handbook/2/generics.html)
- [[Technical-Knowledge/01-Fundamentals/Type-System/TypeScript-Structural-Types|TypeScript Structural Types]]
  - **Official guides and documentation:** [source 1](https://www.typescriptlang.org/docs/handbook/type-compatibility.html)
- [[Technical-Knowledge/01-Fundamentals/Type-System/TypeScript-Type-Narrowing|TypeScript Type Narrowing]]
  - **Official guides and documentation:** [source 1](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)

### 02-Frontend/Next.js

- [[Technical-Knowledge/02-Frontend/Next.js/Next.js-Cache-Boundaries-and-Revalidation|Next.js Cache Boundaries and Revalidation]]
  - **Official guides and documentation:** [source 1](https://nextjs.org/docs/app/guides/caching)
- [[Technical-Knowledge/02-Frontend/Next.js/Next.js-with-TypeScript|Next.js with TypeScript]]
  - **Official guides and documentation:** [source 1](https://nextjs.org/docs)
  - **Release notes and updates:** [source 1](https://nextjs.org/blog)

### 02-Frontend/Nuxt

- [[Technical-Knowledge/02-Frontend/Nuxt/Nuxt|Nuxt]]
  - **Official guides and documentation:** [source 1](https://nuxt.com/docs)
  - **Release notes and updates:** [source 1](https://nuxt.com/blog)
- [[Technical-Knowledge/02-Frontend/Nuxt/Nuxt-Data-Fetching-and-Request-Context|Nuxt Data Fetching and Request Context]]
  - **Official guides and documentation:** [source 1](https://nuxt.com/docs/4.x/getting-started/data-fetching)

### 02-Frontend/React

- [[Technical-Knowledge/02-Frontend/React/React|React]]
  - **Official guides and documentation:** [source 1](https://react.dev/learn)
  - **Release notes and updates:** [source 1](https://react.dev/blog) · [source 2](https://react.dev/blog/2026/09/09/react-19-3)
- [[Technical-Knowledge/02-Frontend/React/React-Component-Composition|React Component Composition]]
  - **Official guides and documentation:** [source 1](https://react.dev/learn/passing-props-to-a-component)
- [[Technical-Knowledge/02-Frontend/React/React-Component-Identity-and-Keys|React Component Identity and Keys]]
  - **Official guides and documentation:** [source 1](https://react.dev/learn/preserving-and-resetting-state)
- [[Technical-Knowledge/02-Frontend/React/React-Effect-Synchronization|React Effect Synchronization]]
  - **Official guides and documentation:** [source 1](https://react.dev/learn/lifecycle-of-reactive-effects)
- [[Technical-Knowledge/02-Frontend/React/React-Rendering-Model|React Rendering Model]]
  - **Official guides and documentation:** [source 1](https://react.dev/learn/render-and-commit)
- [[Technical-Knowledge/02-Frontend/React/React-Server-and-Client-Components|React Server and Client Components]]
  - **API and command reference:** [source 1](https://react.dev/reference/rsc/server-components)
- [[Technical-Knowledge/02-Frontend/React/React-State-and-Batching|React State and Batching]]
  - **Official guides and documentation:** [source 1](https://react.dev/learn/queueing-a-series-of-state-updates)
- [[Technical-Knowledge/02-Frontend/React/React-TypeScript-Props-and-Events|React TypeScript Props and Events]]
  - **Official guides and documentation:** [source 1](https://react.dev/learn/typescript)
- [[Technical-Knowledge/02-Frontend/React/React-with-TypeScript|React with TypeScript]]
  - **Official guides and documentation:** [source 1](https://react.dev/learn/typescript) · [source 2](https://github.com/DefinitelyTyped/DefinitelyTyped/tree/master/types/react)
  - **Release notes and updates:** [source 1](https://react.dev/blog) · [source 2](https://react.dev/blog/2026/09/09/react-19-3)

### 02-Frontend/React-Router

- [[Technical-Knowledge/02-Frontend/React-Router/React-Router-Framework|React Router Framework]]
  - **Official guides and documentation:** [source 1](https://reactrouter.com/start/framework/installation)
  - **Release notes and updates:** [source 1](https://github.com/remix-run/react-router/releases) · [source 2](https://reactrouter.com/changelog)

### 02-Frontend/SvelteKit

- [[Technical-Knowledge/02-Frontend/SvelteKit/Svelte-Runes-and-Reactivity|Svelte Runes and Reactivity]]
  - **Official guides and documentation:** [source 1](https://svelte.dev/docs/svelte/what-are-runes)
- [[Technical-Knowledge/02-Frontend/SvelteKit/SvelteKit|SvelteKit]]
  - **Official guides and documentation:** [source 1](https://svelte.dev/docs/kit/introduction)
  - **Release notes and updates:** [source 1](https://svelte.dev/blog) · [source 2](https://svelte.dev/blog/sveltekit-3-is-here)
- [[Technical-Knowledge/02-Frontend/SvelteKit/SvelteKit-Load-Functions-and-Form-Actions|SvelteKit Load Functions and Form Actions]]
  - **Official guides and documentation:** [source 1](https://svelte.dev/docs/kit/load)

### 02-Frontend/Vite

- [[Technical-Knowledge/02-Frontend/Vite/Vite|Vite]]
  - **Official guides and documentation:** [source 1](https://vite.dev/guide/)
  - **Release notes and updates:** [source 1](https://vite.dev/blog/) · [source 2](https://vite.dev/releases)
- [[Technical-Knowledge/02-Frontend/Vite/Vite-Development-and-Production-Builds|Vite Development and Production Builds]]
  - **Official guides and documentation:** [source 1](https://vite.dev/guide/why.html)

### 02-Frontend/Vue

- [[Technical-Knowledge/02-Frontend/Vue/Vue|Vue]]
  - **Official guides and documentation:** [source 1](https://vuejs.org/guide/introduction.html)
  - **Release notes and updates:** [source 1](https://vuejs.org/about/releases.html)
- [[Technical-Knowledge/02-Frontend/Vue/Vue-Composables|Vue Composables]]
  - **Official guides and documentation:** [source 1](https://vuejs.org/guide/reusability/composables.html)
- [[Technical-Knowledge/02-Frontend/Vue/Vue-Reactivity-and-Computed-State|Vue Reactivity and Computed State]]
  - **Official guides and documentation:** [source 1](https://vuejs.org/guide/essentials/reactivity-fundamentals.html)
- [[Technical-Knowledge/02-Frontend/Vue/Vue-TypeScript-Props-and-Emits|Vue TypeScript Props and Emits]]
  - **Official guides and documentation:** [source 1](https://vuejs.org/guide/typescript/composition-api.html)
- [[Technical-Knowledge/02-Frontend/Vue/Vue-with-TypeScript|Vue with TypeScript]]
  - **Official guides and documentation:** [source 1](https://vuejs.org/guide/typescript/overview.html)
  - **Release notes and updates:** [source 1](https://vuejs.org/about/releases.html)

### 03-Frontend-Libraries

- [[Technical-Knowledge/03-Frontend-Libraries/Browser-Form-State|Browser Form State]]
  - **Official guides and documentation:** [source 1](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms)

### 03-Frontend-Libraries/DaisyUI

- [[Technical-Knowledge/03-Frontend-Libraries/DaisyUI/DaisyUI|DaisyUI]]
  - **Official guides and documentation:** [source 1](https://daisyui.com/docs/) · [source 2](https://github.com/saadeghi/daisyui/blob/master/packages/daisyui/package.json)
  - **Release notes and updates:** [source 1](https://github.com/saadeghi/daisyui/releases)

### 03-Frontend-Libraries/Pinia

- [[Technical-Knowledge/03-Frontend-Libraries/Pinia/Pinia|Pinia]]
  - **Official guides and documentation:** [source 1](https://pinia.vuejs.org/introduction.html)
  - **Release notes and updates:** [source 1](https://github.com/vuejs/pinia/releases)
- [[Technical-Knowledge/03-Frontend-Libraries/Pinia/Pinia-Store-State-Actions-and-Getters|Pinia Store State Actions and Getters]]
  - **Official guides and documentation:** [source 1](https://pinia.vuejs.org/core-concepts/)

### 03-Frontend-Libraries/React-Hook-Form

- [[Technical-Knowledge/03-Frontend-Libraries/React-Hook-Form/React-Hook-Form|React Hook Form]]
  - **Official guides and documentation:** [source 1](https://react-hook-form.com/get-started)
  - **Release notes and updates:** [source 1](https://github.com/react-hook-form/react-hook-form/releases) · [source 2](https://github.com/react-hook-form/resolvers/releases)
- [[Technical-Knowledge/03-Frontend-Libraries/React-Hook-Form/React-Hook-Form-Registration-and-Validation|React Hook Form Registration and Validation]]
  - **Official guides and documentation:** [source 1](https://react-hook-form.com/docs/useform/register)

### 03-Frontend-Libraries/Reka-UI

- [[Technical-Knowledge/03-Frontend-Libraries/Reka-UI/Reka-UI|Reka UI]]
  - **Official guides and documentation:** [source 1](https://reka-ui.com/docs/overview/introduction) · [source 2](https://reka-ui.com/)
  - **Release notes and updates:** [source 1](https://github.com/unovue/reka-ui/releases)

### 03-Frontend-Libraries/Tailwind-CSS

- [[Technical-Knowledge/03-Frontend-Libraries/Tailwind-CSS/Tailwind-CSS|Tailwind CSS]]
  - **Official guides and documentation:** [source 1](https://tailwindcss.com/docs) · [source 2](https://tailwindcss.com/docs/upgrade-guide)
  - **Release notes and updates:** [source 1](https://tailwindcss.com/blog)
- [[Technical-Knowledge/03-Frontend-Libraries/Tailwind-CSS/Utility-First-CSS-and-Design-Tokens|Utility-First CSS and Design Tokens]]
  - **Official guides and documentation:** [source 1](https://tailwindcss.com/docs/theme)

### 03-Frontend-Libraries/TanStack

- [[Technical-Knowledge/03-Frontend-Libraries/TanStack/List-Virtualization-and-Windowing|List Virtualization and Windowing]]
  - **Official guides and documentation:** [source 1](https://tanstack.com/virtual/latest/docs/introduction)
- [[Technical-Knowledge/03-Frontend-Libraries/TanStack/TanStack-Form|TanStack Form]]
  - **Official guides and documentation:** [source 1](https://tanstack.com/form/latest/docs/overview)
  - **Release notes and updates:** [source 1](https://tanstack.com/blog)
- [[Technical-Knowledge/03-Frontend-Libraries/TanStack/TanStack-Query|TanStack Query]]
  - **Official guides and documentation:** [source 1](https://tanstack.com/query/latest/docs/framework/react/overview)
  - **Release notes and updates:** [source 1](https://tanstack.com/blog) · [source 2](https://github.com/TanStack/query/releases)
- [[Technical-Knowledge/03-Frontend-Libraries/TanStack/TanStack-Query-Cache-Lifecycle|TanStack Query Cache Lifecycle]]
  - **Official guides and documentation:** [source 1](https://tanstack.com/query/latest/docs/framework/react/guides/caching)
- [[Technical-Knowledge/03-Frontend-Libraries/TanStack/TanStack-Router|TanStack Router]]
  - **Official guides and documentation:** [source 1](https://tanstack.com/router/latest/docs/framework/react/overview) · [source 2](https://tanstack.com/router/latest/docs/overview)
  - **Release notes and updates:** [source 1](https://tanstack.com/blog) · [source 2](https://tanstack.com/router/latest/docs/blog)
- [[Technical-Knowledge/03-Frontend-Libraries/TanStack/TanStack-Router-Loaders-and-URL-State|TanStack Router Loaders and URL State]]
  - **Official guides and documentation:** [source 1](https://tanstack.com/router/latest/docs/framework/react/guide/data-loading)
- [[Technical-Knowledge/03-Frontend-Libraries/TanStack/TanStack-Table|TanStack Table]]
  - **Official guides and documentation:** [source 1](https://tanstack.com/table/latest/docs/overview)
  - **Release notes and updates:** [source 1](https://tanstack.com/blog)
- [[Technical-Knowledge/03-Frontend-Libraries/TanStack/TanStack-Table-Row-Models-and-Features|TanStack Table Row Models and Features]]
  - **Official guides and documentation:** [source 1](https://tanstack.com/table/latest/docs/guide/row-models)
- [[Technical-Knowledge/03-Frontend-Libraries/TanStack/TanStack-Virtual|TanStack Virtual]]
  - **Official guides and documentation:** [source 1](https://tanstack.com/virtual/latest/docs/introduction)
  - **Release notes and updates:** [source 1](https://tanstack.com/blog) · [source 2](https://github.com/TanStack/virtual/releases)

### 03-Frontend-Libraries/VeeValidate

- [[Technical-Knowledge/03-Frontend-Libraries/VeeValidate/VeeValidate|VeeValidate]]
  - **Official guides and documentation:** [source 1](https://vee-validate.logaretm.com/v4/)
  - **Release notes and updates:** [source 1](https://github.com/logaretm/vee-validate/releases) · [source 2](https://github.com/logaretm/vee-validate/blob/main/CHANGELOG.md)
- [[Technical-Knowledge/03-Frontend-Libraries/VeeValidate/VeeValidate-Form-and-Field-Lifecycle|VeeValidate Form and Field Lifecycle]]
  - **Official guides and documentation:** [source 1](https://vee-validate.logaretm.com/v4/guide/composition-api/getting-started/)

### 03-Frontend-Libraries/Zod

- [[Technical-Knowledge/03-Frontend-Libraries/Zod/Zod|Zod]]
  - **Official guides and documentation:** [source 1](https://zod.dev/)
  - **Release notes and updates:** [source 1](https://github.com/colinhacks/zod/releases)
- [[Technical-Knowledge/03-Frontend-Libraries/Zod/Zod-Runtime-Validation|Zod Runtime Validation]]
  - **Official guides and documentation:** [source 1](https://zod.dev/basics)

### 03-Frontend-Libraries/Zustand

- [[Technical-Knowledge/03-Frontend-Libraries/Zustand/Zustand|Zustand]]
  - **Official guides and documentation:** [source 1](https://zustand.docs.pmnd.rs/getting-started/introduction)
  - **Release notes and updates:** [source 1](https://github.com/pmndrs/zustand/releases)
- [[Technical-Knowledge/03-Frontend-Libraries/Zustand/Zustand-Store-Selectors-and-Persistence|Zustand Store Selectors and Persistence]]
  - **Official guides and documentation:** [source 1](https://zustand.docs.pmnd.rs/integrations/persisting-store-data)

### 04-Backend/Bun

- [[Technical-Knowledge/04-Backend/Bun/Bun|Bun]]
  - **Official guides and documentation:** [source 1](https://bun.sh/docs)
  - **Release notes and updates:** [source 1](https://bun.sh/blog)
- [[Technical-Knowledge/04-Backend/Bun/Bun-Runtime-Compatibility-and-Deployment|Bun Runtime Compatibility and Deployment]]
  - **Release notes and updates:** [source 1](https://bun.sh/blog/bun-v1.4.4)
  - **Official guides and documentation:** [source 1](https://bun.sh/docs/runtime/bun-apis)

### 04-Backend/Elysia

- [[Technical-Knowledge/04-Backend/Elysia/Elysia|Elysia]]
  - **Official guides and documentation:** [source 1](https://elysiajs.com/)
  - **Release notes and updates:** [source 1](https://github.com/elysiajs/elysia/releases) · [source 2](https://next.elysiajs.com/blog/elysia-20-rc/)
- [[Technical-Knowledge/04-Backend/Elysia/Elysia-Schemas-Plugins-and-Type-Inference|Elysia Schemas Plugins and Type Inference]]
  - **Official guides and documentation:** [source 1](https://elysiajs.com/essential/validation)
  - **Release notes and updates:** [source 1](https://next.elysiajs.com/blog/elysia-20-rc/)

### 04-Backend/Express

- [[Technical-Knowledge/04-Backend/Express/Express|Express]]
  - **Official guides and documentation:** [source 1](https://expressjs.com/en/guide/routing.html)
  - **Release notes and updates:** [source 1](https://expressjs.com/en/changelog/) · [source 2](https://github.com/expressjs/express/releases)
- [[Technical-Knowledge/04-Backend/Express/Express-Middleware-Ordering-and-Errors|Express Middleware Ordering and Errors]]
  - **Official guides and documentation:** [source 1](https://expressjs.com/en/guide/using-middleware.html) · [source 2](https://expressjs.com/en/guide/error-handling.html)

### 04-Backend/FastAPI

- [[Technical-Knowledge/04-Backend/FastAPI/FastAPI|FastAPI]]
  - **Official guides and documentation:** [source 1](https://fastapi.tiangolo.com/)
  - **Release notes and updates:** [source 1](https://github.com/fastapi/fastapi/releases) · [source 2](https://fastapi.tiangolo.com/release-notes/)
- [[Technical-Knowledge/04-Backend/FastAPI/FastAPI-Dependency-Injection-and-Lifetimes|FastAPI Dependency Injection and Lifetimes]]
  - **Official guides and documentation:** [source 1](https://fastapi.tiangolo.com/tutorial/dependencies/)

### 04-Backend/Fiber

- [[Technical-Knowledge/04-Backend/Fiber/Fiber|Fiber]]
  - **Official guides and documentation:** [source 1](https://docs.gofiber.io/)
  - **Release notes and updates:** [source 1](https://github.com/gofiber/fiber/releases)

### 04-Backend/Gin

- [[Technical-Knowledge/04-Backend/Gin/Gin|Gin]]
  - **Official guides and documentation:** [source 1](https://gin-gonic.com/en/docs/)
  - **Release notes and updates:** [source 1](https://github.com/gin-gonic/gin/releases)

### 04-Backend/Go

- [[Technical-Knowledge/04-Backend/Go/Go|Go]]
  - **Official guides and documentation:** [source 1](https://go.dev/doc/) · [source 2](https://go.dev/doc/go1.27)
  - **Release notes and updates:** [source 1](https://go.dev/doc/devel/release)
- [[Technical-Knowledge/04-Backend/Go/Go-Channels|Go Channels]]
  - **Official guides and documentation:** [source 1](https://go.dev/tour/concurrency/2)
- [[Technical-Knowledge/04-Backend/Go/Go-Context|Go Context]]
  - **API and command reference:** [source 1](https://pkg.go.dev/context)
- [[Technical-Knowledge/04-Backend/Go/Go-Error-Handling|Go Error Handling]]
  - **Release notes and updates:** [source 1](https://go.dev/blog/error-handling-and-go)
- [[Technical-Knowledge/04-Backend/Go/Go-Goroutines|Go Goroutines]]
  - **Official guides and documentation:** [source 1](https://go.dev/tour/concurrency/1)
- [[Technical-Knowledge/04-Backend/Go/Go-HTTP-Handler-Boundaries|Go HTTP Handler Boundaries]]
  - **API and command reference:** [source 1](https://pkg.go.dev/net/http)

### 04-Backend/Hono

- [[Technical-Knowledge/04-Backend/Hono/Hono|Hono]]
  - **Official guides and documentation:** [source 1](https://hono.dev/docs/)
  - **Release notes and updates:** [source 1](https://github.com/honojs/hono/releases)
- [[Technical-Knowledge/04-Backend/Hono/Hono-Middleware-and-Request-Validation|Hono Middleware and Request Validation]]
  - **Official guides and documentation:** [source 1](https://hono.dev/docs/guides/middleware) · [source 2](https://hono.dev/docs/guides/validation)

### 04-Backend/JavaScript-Runtime

- [[Technical-Knowledge/04-Backend/JavaScript-Runtime/Node.js|Node.js]]
  - **Official guides and documentation:** [source 1](https://nodejs.org/en/learn)

### 04-Backend/Nitro

- [[Technical-Knowledge/04-Backend/Nitro/Nitro|Nitro]]
  - **Official guides and documentation:** [source 1](https://nitro.build/guide)

### 04-Backend/Python

- [[Technical-Knowledge/04-Backend/Python/Python|Python]]
  - **Official guides and documentation:** [source 1](https://docs.python.org/3/tutorial/)

### 05-Database

- [[Technical-Knowledge/05-Database/Database-Connection-Pooling|Database Connection Pooling]]
  - **Official guides and documentation:** [source 1](https://www.postgresql.org/docs/current/runtime-config-connection.html)
- [[Technical-Knowledge/05-Database/PostgreSQL|PostgreSQL]]
  - **Official guides and documentation:** [source 1](https://www.postgresql.org/docs/current/)

### 05-Database/GORM

- [[Technical-Knowledge/05-Database/GORM/GORM|GORM]]
  - **Official guides and documentation:** [source 1](https://gorm.io/docs/)
  - **Release notes and updates:** [source 1](https://github.com/go-gorm/gorm/releases)
- [[Technical-Knowledge/05-Database/GORM/GORM-Transactions-and-Associations|GORM Transactions and Associations]]
  - **Official guides and documentation:** [source 1](https://gorm.io/docs/transactions.html) · [source 2](https://gorm.io/docs/preload.html)

### 05-Database/Prisma

- [[Technical-Knowledge/05-Database/Prisma/Prisma|Prisma]]
  - **Official guides and documentation:** [source 1](https://www.prisma.io/docs)
  - **Release notes and updates:** [source 1](https://www.prisma.io/changelog) · [source 2](https://www.prisma.io/docs/orm/release-status)
- [[Technical-Knowledge/05-Database/Prisma/Prisma-Data-Model-and-Migration-Safety|Prisma Data Model and Migration Safety]]
  - **Release notes and updates:** [source 1](https://www.prisma.io/docs/orm/release-status)
  - **Official guides and documentation:** [source 1](https://www.prisma.io/docs/guides/upgrade-prisma-orm)

### 05-Database/Redis

- [[Technical-Knowledge/05-Database/Redis/Redis|Redis]]
  - **Official guides and documentation:** [source 1](https://redis.io/docs/latest/)
  - **Release notes and updates:** [source 1](https://redis.io/blog/) · [source 2](https://github.com/redis/redis/releases)
- [[Technical-Knowledge/05-Database/Redis/Redis-Cache-Aside|Redis Cache-Aside]]
  - **Official guides and documentation:** [source 1](https://redis.io/docs/latest/develop/use/patterns/)
- [[Technical-Knowledge/05-Database/Redis/Redis-Persistence-and-Durability-Choices|Redis Persistence and Durability Choices]]
  - **Official guides and documentation:** [source 1](https://redis.io/docs/latest/operate/oss_and_stack/management/persistence/)

### 05-Database/sqlc

- [[Technical-Knowledge/05-Database/sqlc/sqlc|sqlc]]
  - **Official guides and documentation:** [source 1](https://docs.sqlc.dev/en/latest/)
  - **Release notes and updates:** [source 1](https://github.com/sqlc-dev/sqlc/releases)
- [[Technical-Knowledge/05-Database/sqlc/sqlc-Query-Contracts-and-Generated-Code|sqlc Query Contracts and Generated Code]]
  - **Official guides and documentation:** [source 1](https://docs.sqlc.dev/en/latest/howto/transactions.html)
  - **API and command reference:** [source 1](https://docs.sqlc.dev/en/latest/reference/config.html)

### 06-Security

- [[Technical-Knowledge/06-Security/Cookie-and-Session-Security|Cookie and Session Security]]
  - **Official guides and documentation:** [source 1](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Cookies)
- [[Technical-Knowledge/06-Security/HTTP-Authentication|HTTP Authentication]]
  - **Official guides and documentation:** [source 1](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication)
- [[Technical-Knowledge/06-Security/JWT-Validation|JWT Validation]]
  - **Standards and specifications:** [source 1](https://www.rfc-editor.org/rfc/rfc8725)
- [[Technical-Knowledge/06-Security/OAuth-Authorization-Code-with-PKCE|OAuth Authorization Code with PKCE]]
  - **Standards and specifications:** [source 1](https://www.rfc-editor.org/rfc/rfc9700)
- [[Technical-Knowledge/06-Security/Session-Management|Session Management]]
  - **Official guides and documentation:** [source 1](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Cookies)

### 06-Security/JWT

- [[Technical-Knowledge/06-Security/JWT/JWT|JWT]]
  - **Standards and specifications:** [source 1](https://www.rfc-editor.org/rfc/rfc7519) · [source 2](https://www.rfc-editor.org/rfc/rfc8725)

### 06-Security/OAuth-2.0

- [[Technical-Knowledge/06-Security/OAuth-2.0/OAuth-2.0|OAuth 2.0]]
  - **Standards and specifications:** [source 1](https://www.rfc-editor.org/rfc/rfc6749) · [source 2](https://www.rfc-editor.org/rfc/rfc9700)

### 07-Testing

- [[Technical-Knowledge/07-Testing/Unit-Integration-and-End-to-End-Tests|Unit Integration and End-to-End Tests]]
  - **Official guides and documentation:** [source 1](https://martinfowler.com/articles/practical-test-pyramid.html)

### 07-Testing/Go-Testing

- [[Technical-Knowledge/07-Testing/Go-Testing/Go-Table-Driven-Tests|Go Table-Driven Tests]]
  - **Official guides and documentation:** [source 1](https://go.dev/doc/tutorial/add-a-test)
- [[Technical-Knowledge/07-Testing/Go-Testing/Go-Testing|Go Testing]]
  - **Official guides and documentation:** [source 1](https://go.dev/doc/tutorial/add-a-test)
  - **Release notes and updates:** [source 1](https://go.dev/doc/devel/release)

### 07-Testing/Playwright

- [[Technical-Knowledge/07-Testing/Playwright/Playwright|Playwright]]
  - **Official guides and documentation:** [source 1](https://playwright.dev/docs/intro)
  - **Release notes and updates:** [source 1](https://playwright.dev/docs/release-notes)
- [[Technical-Knowledge/07-Testing/Playwright/Playwright-Locators-and-Auto-Waiting|Playwright Locators and Auto-Waiting]]
  - **Official guides and documentation:** [source 1](https://playwright.dev/docs/locators)

### 07-Testing/Vitest

- [[Technical-Knowledge/07-Testing/Vitest/Vitest|Vitest]]
  - **Official guides and documentation:** [source 1](https://vitest.dev/guide/) · [source 2](https://vitest.dev/guide/migration/)
  - **Release notes and updates:** [source 1](https://vitest.dev/blog/)

### 08-Infrastructure/Docker

- [[Technical-Knowledge/08-Infrastructure/Docker/Docker|Docker]]
  - **Official guides and documentation:** [source 1](https://docs.docker.com/) · [source 2](https://docs.docker.com/build/)
  - **Release notes and updates:** [source 1](https://docs.docker.com/engine/release-notes/)
- [[Technical-Knowledge/08-Infrastructure/Docker/Docker-Image-Layers-and-Reproducible-Builds|Docker Image Layers and Reproducible Builds]]
  - **Official guides and documentation:** [source 1](https://docs.docker.com/build/building/best-practices/)

### 08-Infrastructure/Docker-Compose

- [[Technical-Knowledge/08-Infrastructure/Docker-Compose/Docker-Compose|Docker Compose]]
  - **Official guides and documentation:** [source 1](https://docs.docker.com/compose/)
  - **Release notes and updates:** [source 1](https://docs.docker.com/compose/release-notes/)
- [[Technical-Knowledge/08-Infrastructure/Docker-Compose/Docker-Compose-Service-Networking-and-Health|Docker Compose Service Networking and Health]]
  - **Official guides and documentation:** [source 1](https://docs.docker.com/compose/how-tos/networking/)

### 08-Infrastructure/Nginx

- [[Technical-Knowledge/08-Infrastructure/Nginx/Nginx|Nginx]]
  - **Official guides and documentation:** [source 1](https://nginx.org/en/docs/) · [source 2](https://nginx.org/en/CHANGES) · [source 3](https://nginx.org/en/download.html) · [source 4](https://nginx.org/en/)
- [[Technical-Knowledge/08-Infrastructure/Nginx/Nginx-Reverse-Proxy-Request-Flow|Nginx Reverse Proxy Request Flow]]
  - **Official guides and documentation:** [source 1](https://nginx.org/en/docs/http/ngx_http_proxy_module.html) · [source 2](http://api:8080/)

### 08-Infrastructure/RabbitMQ

- [[Technical-Knowledge/08-Infrastructure/RabbitMQ/RabbitMQ|RabbitMQ]]
  - **Official guides and documentation:** [source 1](https://www.rabbitmq.com/docs)
  - **Release notes and updates:** [source 1](https://www.rabbitmq.com/changelog.html) · [source 2](https://www.rabbitmq.com/release-information)
- [[Technical-Knowledge/08-Infrastructure/RabbitMQ/RabbitMQ-Acknowledgements-and-Redelivery|RabbitMQ Acknowledgements and Redelivery]]
  - **Official guides and documentation:** [source 1](https://www.rabbitmq.com/docs/confirms)

### 09-Architecture/API-Design

- [[Technical-Knowledge/09-Architecture/API-Design/HTTP-Semantics-and-REST|HTTP Semantics and REST]]
  - **Standards and specifications:** [source 1](https://www.rfc-editor.org/rfc/rfc9110)
- [[Technical-Knowledge/09-Architecture/API-Design/OpenAPI|OpenAPI]]
  - **Official guides and documentation:** [source 1](https://spec.openapis.org/oas/latest.html)

### 09-Architecture/Application-Architecture

- [[Technical-Knowledge/09-Architecture/Application-Architecture/State-Management-Concepts|State Management Concepts]]
  - **Official guides and documentation:** [source 1](https://react.dev/learn/sharing-state-between-components)

### 11-References

- [[Technical-Knowledge/11-References/Technology-Overview-Template|Technology Name]]
  - **Official guides and documentation:** [source 1](https://official-docs.example/)
  - **Release notes and updates:** [source 1](https://official-docs.example/releases)

### 12-Command-Reference/Bun

- [[Technical-Knowledge/12-Command-Reference/Bun/Bun-Recipes|Bun Recipes]]
  - **Official guides and documentation:** [source 1](https://bun.sh/docs) · [source 2](https://bun.sh/docs/runtime/http/server)

### 12-Command-Reference/DaisyUI

- [[Technical-Knowledge/12-Command-Reference/DaisyUI/DaisyUI-Recipes|DaisyUI Recipes]]
  - **Official guides and documentation:** [source 1](https://daisyui.com/docs/install/) · [source 2](https://daisyui.com/docs/themes/)

### 12-Command-Reference/Docker

- [[Technical-Knowledge/12-Command-Reference/Docker/Docker-Recipes|Docker Recipes]]
  - **Official guides and documentation:** [source 1](https://docs.docker.com/get-started/docker-concepts/building-images/writing-a-dockerfile/)
  - **API and command reference:** [source 1](https://docs.docker.com/reference/cli/docker/)

### 12-Command-Reference/Docker-Compose

- [[Technical-Knowledge/12-Command-Reference/Docker-Compose/Docker-Compose-Recipes|Docker Compose Recipes]]
  - **Official guides and documentation:** [source 1](https://docs.docker.com/compose/gettingstarted/)
  - **API and command reference:** [source 1](https://docs.docker.com/reference/cli/docker/compose/)

### 12-Command-Reference/Elysia

- [[Technical-Knowledge/12-Command-Reference/Elysia/Elysia-Recipes|Elysia Recipes]]
  - **Official guides and documentation:** [source 1](https://elysiajs.com/)
  - **Release notes and updates:** [source 1](https://github.com/elysiajs/elysia/releases)

### 12-Command-Reference/Express

- [[Technical-Knowledge/12-Command-Reference/Express/Express-Recipes|Express Recipes]]
  - **Official guides and documentation:** [source 1](https://expressjs.com/en/guide/routing.html) · [source 2](https://expressjs.com/en/guide/error-handling.html)

### 12-Command-Reference/FastAPI

- [[Technical-Knowledge/12-Command-Reference/FastAPI/FastAPI-Recipes|FastAPI Recipes]]
  - **Official guides and documentation:** [source 1](https://fastapi.tiangolo.com/tutorial/) · [source 2](https://fastapi.tiangolo.com/tutorial/dependencies/)

### 12-Command-Reference/Fiber

- [[Technical-Knowledge/12-Command-Reference/Fiber/Fiber-Recipes|Fiber Recipes]]
  - **Official guides and documentation:** [source 1](https://docs.gofiber.io/)
  - **Release notes and updates:** [source 1](https://github.com/gofiber/fiber/releases)

### 12-Command-Reference/GORM

- [[Technical-Knowledge/12-Command-Reference/GORM/GORM-Recipes|GORM Recipes]]
  - **Official guides and documentation:** [source 1](https://gorm.io/docs/) · [source 2](https://gorm.io/docs/transactions.html)

### 12-Command-Reference/Gin

- [[Technical-Knowledge/12-Command-Reference/Gin/Gin-Recipes|Gin Recipes]]
  - **Official guides and documentation:** [source 1](https://gin-gonic.com/en/docs/)
  - **Release notes and updates:** [source 1](https://github.com/gin-gonic/gin/releases)

### 12-Command-Reference/Go

- [[Technical-Knowledge/12-Command-Reference/Go/Go-Recipes|Go Recipes]]
  - **Official guides and documentation:** [source 1](https://go.dev/doc/)

### 12-Command-Reference/Go-Testing

- [[Technical-Knowledge/12-Command-Reference/Go-Testing/Go-Testing-Recipes|Go Testing Recipes]]
  - **Official guides and documentation:** [source 1](https://go.dev/doc/tutorial/add-a-test)
  - **API and command reference:** [source 1](https://pkg.go.dev/testing)

### 12-Command-Reference/Hono

- [[Technical-Knowledge/12-Command-Reference/Hono/Hono-Recipes|Hono Recipes]]
  - **Official guides and documentation:** [source 1](https://hono.dev/docs/) · [source 2](https://hono.dev/docs/guides/validation)

### 12-Command-Reference/JWT

- [[Technical-Knowledge/12-Command-Reference/JWT/JWT-Recipes|JWT Recipes]]
  - **Standards and specifications:** [source 1](https://www.rfc-editor.org/rfc/rfc7519) · [source 2](https://www.rfc-editor.org/rfc/rfc8725)

### 12-Command-Reference/JavaScript

- [[Technical-Knowledge/12-Command-Reference/JavaScript/JavaScript-Recipes|JavaScript Recipes]]
  - **Official guides and documentation:** [source 1](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

### 12-Command-Reference/Next.js

- [[Technical-Knowledge/12-Command-Reference/Next.js/Nextjs-Recipes|Next.js Recipes]]
  - **Official guides and documentation:** [source 1](https://nextjs.org/docs)

### 12-Command-Reference/Nginx

- [[Technical-Knowledge/12-Command-Reference/Nginx/Nginx-Recipes|Nginx Recipes]]
  - **Official guides and documentation:** [source 1](https://nginx.org/en/docs/beginners_guide.html) · [source 2](https://nginx.org/en/docs/http/ngx_http_proxy_module.html) · [source 3](http://app:3000)

### 12-Command-Reference/Nuxt

- [[Technical-Knowledge/12-Command-Reference/Nuxt/Nuxt-Recipes|Nuxt Recipes]]
  - **Official guides and documentation:** [source 1](https://nuxt.com/docs/4.x/getting-started/introduction)
  - **API and command reference:** [source 1](https://nuxt.com/docs/4.x/api/composables/use-fetch)

### 12-Command-Reference/OAuth-2.0

- [[Technical-Knowledge/12-Command-Reference/OAuth-2.0/OAuth-Recipes|OAuth 2.0 Recipes]]
  - **Standards and specifications:** [source 1](https://www.rfc-editor.org/rfc/rfc9700) · [source 2](https://www.rfc-editor.org/rfc/rfc7636)

### 12-Command-Reference/Pinia

- [[Technical-Knowledge/12-Command-Reference/Pinia/Pinia-Recipes|Pinia Recipes]]
  - **Official guides and documentation:** [source 1](https://pinia.vuejs.org/core-concepts/)

### 12-Command-Reference/Playwright

- [[Technical-Knowledge/12-Command-Reference/Playwright/Playwright-Recipes|Playwright Recipes]]
  - **Official guides and documentation:** [source 1](https://playwright.dev/docs/intro) · [source 2](https://playwright.dev/docs/locators)

### 12-Command-Reference/Prisma

- [[Technical-Knowledge/12-Command-Reference/Prisma/Prisma-Recipes|Prisma Recipes]]
  - **Official guides and documentation:** [source 1](https://www.prisma.io/docs/orm/prisma-schema/overview) · [source 2](https://www.prisma.io/docs/orm/prisma-client/queries/transactions)

### 12-Command-Reference/Python

- [[Technical-Knowledge/12-Command-Reference/Python/Python-Recipes|Python Recipes]]
  - **Official guides and documentation:** [source 1](https://docs.python.org/3/tutorial/) · [source 2](https://docs.python.org/3/library/)

### 12-Command-Reference/RabbitMQ

- [[Technical-Knowledge/12-Command-Reference/RabbitMQ/RabbitMQ-Recipes|RabbitMQ Recipes]]
  - **Official guides and documentation:** [source 1](https://www.rabbitmq.com/tutorials) · [source 2](https://www.rabbitmq.com/docs/confirms)

### 12-Command-Reference/React

- [[Technical-Knowledge/12-Command-Reference/React/React-Recipes|React Recipes]]
  - **API and command reference:** [source 1](https://react.dev/reference/react)

### 12-Command-Reference/React-Hook-Form

- [[Technical-Knowledge/12-Command-Reference/React-Hook-Form/React-Hook-Form-Recipes|React Hook Form Recipes]]
  - **Official guides and documentation:** [source 1](https://react-hook-form.com/get-started) · [source 2](https://github.com/react-hook-form/resolvers)

### 12-Command-Reference/React-Router

- [[Technical-Knowledge/12-Command-Reference/React-Router/React-Router-Recipes|React Router Recipes]]
  - **Official guides and documentation:** [source 1](https://reactrouter.com/start/framework/installation) · [source 2](https://reactrouter.com/start/framework/data-loading)

### 12-Command-Reference/React-with-TypeScript

- [[Technical-Knowledge/12-Command-Reference/React-with-TypeScript/React-TypeScript-Recipes|React with TypeScript Recipes]]
  - **Official guides and documentation:** [source 1](https://react.dev/learn/typescript) · [source 2](https://www.typescriptlang.org/docs/)

### 12-Command-Reference/Redis

- [[Technical-Knowledge/12-Command-Reference/Redis/Redis-Recipes|Redis Recipes]]
  - **Official guides and documentation:** [source 1](https://redis.io/docs/latest/develop/)
  - **API and command reference:** [source 1](https://redis.io/docs/latest/commands/)

### 12-Command-Reference/Reka-UI

- [[Technical-Knowledge/12-Command-Reference/Reka-UI/Reka-UI-Recipes|Reka UI Recipes]]
  - **Official guides and documentation:** [source 1](https://reka-ui.com/docs/overview/introduction) · [source 2](https://reka-ui.com/docs/components/dialog)

### 12-Command-Reference/SQL

- [[Technical-Knowledge/12-Command-Reference/SQL/SQL-Recipes|SQL Recipes]]
  - **Official guides and documentation:** [source 1](https://www.postgresql.org/docs/current/tutorial.html) · [source 2](https://www.postgresql.org/docs/current/sql.html)

### 12-Command-Reference/SvelteKit

- [[Technical-Knowledge/12-Command-Reference/SvelteKit/SvelteKit-Recipes|SvelteKit Recipes]]
  - **Official guides and documentation:** [source 1](https://svelte.dev/docs/kit)

### 12-Command-Reference/Tailwind-CSS

- [[Technical-Knowledge/12-Command-Reference/Tailwind-CSS/Tailwind-Recipes|Tailwind CSS Recipes]]
  - **Official guides and documentation:** [source 1](https://tailwindcss.com/docs/installation) · [source 2](https://tailwindcss.com/docs/styling-with-utility-classes)

### 12-Command-Reference/TanStack

- [[Technical-Knowledge/12-Command-Reference/TanStack/TanStack-Form-Recipes|TanStack Form Recipes]]
  - **Official guides and documentation:** [source 1](https://tanstack.com/form/latest/docs/framework/react/overview)
  - **Release notes and updates:** [source 1](https://tanstack.com/blog/announcing-tanstack-form-v2-alpha)
- [[Technical-Knowledge/12-Command-Reference/TanStack/TanStack-Query-Recipes|TanStack Query Recipes]]
  - **Official guides and documentation:** [source 1](https://tanstack.com/query/latest/docs/framework/react/overview) · [source 2](https://tanstack.com/query/latest/docs/framework/react/guides/invalidations-from-mutations)
- [[Technical-Knowledge/12-Command-Reference/TanStack/TanStack-Router-Recipes|TanStack Router Recipes]]
  - **Official guides and documentation:** [source 1](https://tanstack.com/router/latest/docs/framework/react/overview)
- [[Technical-Knowledge/12-Command-Reference/TanStack/TanStack-Table-Recipes|TanStack Table Recipes]]
  - **Official guides and documentation:** [source 1](https://tanstack.com/table/latest/docs/guide/introduction)
- [[Technical-Knowledge/12-Command-Reference/TanStack/TanStack-Virtual-Recipes|TanStack Virtual Recipes]]
  - **Official guides and documentation:** [source 1](https://tanstack.com/virtual/latest/docs/introduction)

### 12-Command-Reference/TypeScript

- [[Technical-Knowledge/12-Command-Reference/TypeScript/TypeScript-Recipes|TypeScript Recipes]]
  - **Official guides and documentation:** [source 1](https://www.typescriptlang.org/docs/)

### 12-Command-Reference/VeeValidate

- [[Technical-Knowledge/12-Command-Reference/VeeValidate/VeeValidate-Recipes|VeeValidate Recipes]]
  - **Official guides and documentation:** [source 1](https://vee-validate.logaretm.com/v4/guide/composition-api/getting-started/) · [source 2](https://vee-validate.logaretm.com/v4/guide/components/validation)

### 12-Command-Reference/Vite

- [[Technical-Knowledge/12-Command-Reference/Vite/Vite-Recipes|Vite Recipes]]
  - **Official guides and documentation:** [source 1](https://vite.dev/guide/) · [source 2](https://vite.dev/config/) · [source 3](http://localhost:3000)

### 12-Command-Reference/Vitest

- [[Technical-Knowledge/12-Command-Reference/Vitest/Vitest-Recipes|Vitest Recipes]]
  - **Official guides and documentation:** [source 1](https://vitest.dev/guide/)
  - **API and command reference:** [source 1](https://vitest.dev/api/)

### 12-Command-Reference/Vue

- [[Technical-Knowledge/12-Command-Reference/Vue/Vue-API-Recipes|Vue API Recipes]]
  - **API and command reference:** [source 1](https://vuejs.org/api/reactivity-core.html)
  - **Official guides and documentation:** [source 1](https://vuejs.org/guide/essentials/reactivity-fundamentals.html) · [source 2](https://vuejs.org/guide/essentials/watchers.html) · [source 3](https://vuejs.org/guide/components/props.html) · [source 4](https://vuejs.org/guide/components/events.html) · [source 5](https://vuejs.org/guide/reusability/composables.html)

### 12-Command-Reference/Vue-with-TypeScript

- [[Technical-Knowledge/12-Command-Reference/Vue-with-TypeScript/Vue-TypeScript-Recipes|Vue with TypeScript Recipes]]
  - **Official guides and documentation:** [source 1](https://vuejs.org/guide/typescript/overview.html) · [source 2](https://vuejs.org/guide/typescript/composition-api.html)

### 12-Command-Reference/Zod

- [[Technical-Knowledge/12-Command-Reference/Zod/Zod-Recipes|Zod Recipes]]
  - **Official guides and documentation:** [source 1](https://zod.dev/basics) · [source 2](https://zod.dev/api)

### 12-Command-Reference/Zustand

- [[Technical-Knowledge/12-Command-Reference/Zustand/Zustand-Recipes|Zustand Recipes]]
  - **Official guides and documentation:** [source 1](https://zustand.docs.pmnd.rs/getting-started/introduction)

### 12-Command-Reference/sqlc

- [[Technical-Knowledge/12-Command-Reference/sqlc/sqlc-Recipes|sqlc Recipes]]
  - **Official guides and documentation:** [source 1](https://docs.sqlc.dev/en/latest/) · [source 2](https://docs.sqlc.dev/en/latest/howto/parameters.html)
