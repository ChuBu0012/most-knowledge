---
title: Next.js Recipes
type: reference
tags: [technical-knowledge, api-reference, recipes, nextjs]
status: researched
last_verified: 2026-11-20
sources:
  - https://nextjs.org/docs
---

# Next.js Recipes

ตัวอย่าง App Router สำหรับงานที่พบบ่อย ตรวจ signature ให้ตรง Next major ในโปรเจกต์

## สร้างโปรเจกต์

```sh
npx create-next-app@latest my-app --ts --app
cd my-app
npm run dev
```

## สร้างหน้าและอ่าน route param

สร้าง `app/products/[id]/page.tsx` แล้วอ่าน params จาก page props ตาม type ของ Next รุ่นที่ใช้. โหลดข้อมูลใน Server Component เป็นค่าเริ่มต้น; ไม่ใส่ `"use client"` หากไม่ต้องใช้ browser state/event.

```tsx
export default async function ProductPage({ params }: { params: Promise<{ id: string }> }) {
  const { id } = await params
  const product = await getProduct(id)
  if (!product) notFound()
  return <ProductView product={product} />
}
```

## เพิ่ม interaction ฝั่ง browser

ใส่ `"use client"` ไว้บนสุดของไฟล์ที่มี state/event; จำกัด boundary ให้อยู่ subtree เล็ก ส่งข้อมูลที่ serialize ได้จาก server ลง client และไม่ส่ง secret.

```tsx
"use client"
import { useState } from 'react'
export function Quantity() {
  const [count, setCount] = useState(1)
  return <button onClick={() => setCount(n => n + 1)}>{count}</button>
}
```

## ทำ mutation ด้วย Server Action

ตรวจ auth และ validate ข้อมูลภายใน action ทุกครั้ง จากนั้น mutate แล้ว revalidate cache ตามข้อมูลที่เปลี่ยน.

```ts
'use server'
import { revalidatePath } from 'next/cache'
export async function renameProduct(formData: FormData) {
  const user = await requireUser()
  const id = String(formData.get('id') ?? '')
  const name = String(formData.get('name') ?? '').trim()
  if (!id || !name) throw new Error('Invalid input')
  await updateProductForUser(user.id, id, name)
  revalidatePath(`/products/${id}`)
}
```

การซ่อนปุ่มหรือจำกัดหน้า UI ไม่ใช่ authorization; ตรวจ ownership ที่ server.

## อ่าน search params

ใช้ URL สำหรับ filter, pagination และ sort ที่ควร bookmark/share/back-forward. Parse และ clamp ค่า เช่น page ให้เป็นจำนวนเต็มบวกก่อน query database.

## เลือก cache และ revalidation

ระบุความสดที่ต้องการตาม data; หลัง mutation ใช้ `revalidatePath` หรือ `revalidateTag` สำหรับขอบเขตที่เปลี่ยน. แยก cache ที่ผูกกับผู้ใช้ออกจาก public data และตรวจ Cache Components ตามรุ่น Next ที่ติดตั้ง.

## จัดการ redirect / not found

เรียก `redirect('/login')` หรือ `notFound()` จาก `next/navigation` ใน boundary ที่เหมาะสม. อย่ากลืน special control-flow error เหล่านี้ด้วย catch กว้าง.

## รัน production build

```sh
npm run build
npm run start
```

ทำ build ใน CI เพื่อจับปัญหา server/client boundary และ environment ก่อน deploy.

## อ่านต่อ

[[Next.js Cache Boundaries and Revalidation]] · [[React Server and Client Components]] · [[React Recipes]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
