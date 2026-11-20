---
title: "React Hook Form Registration and Validation"
type: concept
domain: react hook form
level: intermediate
tags: [react-hook-form, forms, react]
status: researched
last_verified: 2026-11-20
sources:
  - https://react-hook-form.com/docs/useform/register
---

# React Hook Form Registration and Validation

## Overview

React Hook Form ใช้ form control/registration เก็บค่าจาก inputs โดยลดการ rerender ทั้งฟอร์ม; resolver เชื่อม schema validation

## Mental model

`register` ต่อ uncontrolled input กับ form state; `Controller` bridge controlled component ที่ต้องรับ `value`/`onChange`. `handleSubmit` รวบรวม/validate payload แล้วเรียก success/error callback. `formState` ใช้ subscription proxy; อ่านเฉพาะ state ที่ต้องใช้เพื่อลด updates

## Example

```tsx
const { register, handleSubmit, formState: { errors } } = useForm<FormInput>({
  resolver: zodResolver(schema),
});
<form onSubmit={handleSubmit(save)}>
  <input {...register('email')} />
  {errors.email && <p>{errors.email.message}</p>}
</form>
```

Snippet is a focused pattern; include package imports, types, error handling, validation and runtime configuration from the installed release before production use.

## Common mistakes and trade-offs

ใช้ register กับ controlled widget โดยตรงอาจทำให้ค่าหลุด; defaultValues ต้องสอดคล้อง type/schema; client resolver ไม่แทน server validation; reset/async defaults ต้องจัด lifecycle

## Practical guidance

เก็บ schema ร่วมกับ server เมื่อเหมาะสม, map server errors ด้วย `setError`, ป้องกัน submit ซ้ำและทดสอบ keyboard/labels/errors ด้วย browser tests

## Related knowledge

[[React-Hook-Form]] · [[Browser Form State]] · [[Zod Runtime Validation]] · [[Playwright Locators and Auto-Waiting]]

## References

- [react-hook-form.com](https://react-hook-form.com/docs/useform/register)
