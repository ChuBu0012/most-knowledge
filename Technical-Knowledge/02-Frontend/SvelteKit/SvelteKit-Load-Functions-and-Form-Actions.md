---
title: "SvelteKit Load Functions and Form Actions"
type: concept
domain: sveltekit
level: intermediate
tags: [sveltekit, data-fetching, forms]
status: researched
last_verified: 2026-11-20
sources:
  - https://svelte.dev/docs/kit/load
---

# SvelteKit Load Functions and Form Actions

## Overview

SvelteKit ใช้ `load` เติมข้อมูลตาม route และ form actions รับ mutation แบบ progressive enhancement; server/client load ต่างกันเรื่อง trust และ capabilities

## Mental model

`+page.server`/`+layout.server` รัน server-side; universal `load` อาจรันทั้ง server และ browser. `load` รับ params/url/fetch/parent และคืน data serializable. Form actions รับ POST จาก form; `use:enhance` เพิ่ม UX โดยยังมี HTML form fallback. ใช้ `fail` สำหรับ validation result ที่ไม่ใช่ exception

## Example

```svelte
// +page.server.ts — schematic
export const actions = {
  default: async ({ request, locals }) => {
    const form = await request.formData();
    const title = String(form.get('title') ?? '');
    if (!title.trim()) return fail(400, { title, missing: true });
    await locals.db.createPost({ title });
    return { success: true };
  }
};
```

Snippet is a focused pattern; include package imports, types, error handling, validation and runtime configuration from the installed release before production use.

## Common mistakes and trade-offs

ข้อมูล `load` ที่ส่งถึง browser ต้องไม่รวม secret; authorize mutation ใน action ทุกครั้ง; `load` ที่เรียก API แบบไม่ระวังอาจเกิด SSRF/credential leak; form action error response ต้องแยก validation จาก server failure

## Practical guidance

ใช้ server load สำหรับ secret/database, validate `FormData` runtime, progressive enhancement, redirect/invalidate after mutation, and ensure CSRF/access-control behavior for chosen adapter

## Related knowledge

[[SvelteKit]] · [[Svelte Runes and Reactivity]] · [[Browser Form State]] · [[OAuth-2.0]]

## References

- [svelte.dev](https://svelte.dev/docs/kit/load)
