---
title: Vite Recipes
type: reference
tags: [technical-knowledge, vite, build-tool, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://vite.dev/guide/
  - https://vite.dev/config/
---

# Vite Recipes

## Scaffold and run

```sh
npm create vite@latest my-app -- --template vue-ts
cd my-app
npm install
npm run dev
```

Choose matching framework template; Vite supplies dev server/build, not the application router/backend.

## Configure API proxy

```ts
export default defineConfig({
  server: { proxy: { '/api': { target: 'http://localhost:3000', changeOrigin: true } } },
})
```

Dev proxy does not configure production ingress. Avoid treating it as a security boundary.

## Environment variables

Read `import.meta.env.MODE`, `DEV`, `PROD`. Client-facing custom values require `VITE_` prefix and are embedded in bundle; never put secrets there.

## Alias paths

Set `resolve.alias` in Vite and matching `compilerOptions.paths` in TypeScript config. Keep aliases consistent with test runner/editor.

## Build and preview

```sh
npm run build
npm run preview
```

Deploy generated `dist` for static app; configure SPA fallback only if client router needs it. Review plugin compatibility for current Vite/Rolldown line.

## Read next

[[Vite Development and Production Builds]] · [[Vitest Recipes]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
