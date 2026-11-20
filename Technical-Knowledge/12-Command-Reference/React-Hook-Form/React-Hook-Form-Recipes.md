---
title: React Hook Form Recipes
type: reference
tags: [technical-knowledge, react-hook-form, react, forms, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://react-hook-form.com/get-started
  - https://github.com/react-hook-form/resolvers
---

# React Hook Form Recipes

## Register native inputs and submit

```tsx
const { register, handleSubmit, formState: { errors, isSubmitting } } = useForm<FormValues>()
const onSubmit = async (values: FormValues) => save(values)
return <form onSubmit={handleSubmit(onSubmit)}>
  <input {...register('email', { required: 'Email is required' })} />
  {errors.email && <p role="alert">{errors.email.message}</p>}
  <button disabled={isSubmitting}>Save</button>
</form>
```

`register` wires ref/name/events; native controls stay mostly uncontrolled. Render accessible error text and prevent duplicate submits while pending.

## Validate with schema resolver

```tsx
const form = useForm<FormInput, unknown, FormOutput>({ resolver: zodResolver(schema) })
```

Resolver transforms/validates values; distinguish input values from parsed output when schema transforms strings. Keep server-side validation too.

## Controlled third-party widget

Use `Controller`/`useController` for components that require `value` and `onChange`; do not both `register` and `Controller` the same field. Map widget value types explicitly.

## Field arrays

`useFieldArray({ control, name: 'items' })`; render rows with `field.id` as React key; call `append`, `remove`, `move`. Avoid array index as key and avoid mutating fields directly.

## Reset and server errors

Call `reset(serverValues)` after successful save when new values become baseline. Map server field errors with `setError`; clear/reconcile them when inputs change. Beware stale asynchronous validation responses; ensure the latest submission owns displayed errors.

## Read next

[[React Hook Form Registration and Validation]] · [[Zod Recipes]] · [[Browser Form State]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
