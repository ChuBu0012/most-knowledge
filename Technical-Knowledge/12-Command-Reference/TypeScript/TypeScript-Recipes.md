---
title: "TypeScript Recipes"
type: reference
domain: typescript
tags: [technical-knowledge, api-reference, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://www.typescriptlang.org/docs/
---

# TypeScript Recipes

คู่มือค้นจากงานที่ต้องทำ ตัวอย่างมุ่งที่ API/คำสั่งที่ใช้บ่อย; ตรวจ runtime/compiler version ในโปรเจกต์ก่อนใช้

## ระบุชนิดข้อมูลและ function contract

```ts
type User = { id: string; name: string; email?: string };
function findUser(users: User[], id: User['id']): User | undefined {
  return users.find(user => user.id === id);
}
```

ใช้ `type` กับ union/composition; `interface` เหมาะกับ object contract ที่ต้อง extend/merge. Optional `email?` หมายถึงอาจไม่มี property; ไม่เท่ากับ `email: string | null`.

## ทำ function ใช้ได้หลาย type ด้วย generic

```ts
function first<T>(items: readonly T[]): T | undefined { return items[0]; }
const user = first([{ id: 'u1', name: 'Ada' }]); // T อนุมานเป็น object
```

Generic ควรรักษาความสัมพันธ์ระหว่าง input/output; อย่าแทนทุกอย่างด้วย `any`. ใช้ `unknown` ที่ขอบเขตข้อมูลแล้ว narrow ก่อนใช้.

## แยก variant ด้วย discriminated union

```ts
type Result<T> = { ok: true; value: T } | { ok: false; error: Error };
function unwrap<T>(result: Result<T>): T {
  if (result.ok) return result.value;
  throw result.error;
}
```

Literal tag (`ok`) ทำให้ control-flow narrowing แยก branch ได้. เพิ่ม `never` exhaustiveness check ใน switch เมื่อ union ต้องจัดการครบทุก variant.

## parse `unknown` อย่างปลอดภัย

```ts
function isUser(value: unknown): value is User {
  return typeof value === 'object' && value !== null &&
    'id' in value && typeof value.id === 'string' &&
    'name' in value && typeof value.name === 'string';
}
const raw: unknown = JSON.parse(text);
if (!isUser(raw)) throw new Error('Invalid user payload');
```

Type guard ต้องตรวจสิ่งที่โค้ดจะอ่านจริง; assertion `as User` ไม่ได้ validate. สำหรับ schema ซับซ้อนใช้ runtime validator เช่น [[Zod Runtime Validation]].

## เลือก optional chaining/nullish defaults

```ts
const city = response.user?.address?.city ?? 'Unknown';
```

`?.` หยุดเมื่อ null/undefined; `??` ใช้ default เฉพาะ nullish ไม่กลบค่า `0`, `false`, หรือ `''` แบบ `||`.

## รับชนิดจาก object ด้วย `typeof` / `keyof`

```ts
const config = { retries: 3, mode: 'safe' } as const;
type Config = typeof config;
type ConfigKey = keyof Config;
```

ใช้ `satisfies` ตรวจ object กับ contract โดยยังเก็บ literal inference: `const routes = { home: '/' } satisfies Record<string, string>`. ใช้ `as const` เมื่อค่าควรเป็น readonly literal.

## ค้นต่อ

[[TypeScript Type Narrowing]] · [[TypeScript Generics]] · [[TypeScript Structural Types]] · [[Zod Runtime Validation]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
