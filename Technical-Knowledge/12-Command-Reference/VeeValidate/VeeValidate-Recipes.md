---
title: VeeValidate Recipes
type: reference
tags: [technical-knowledge, vee-validate, vue, forms, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://vee-validate.logaretm.com/v4/guide/composition-api/getting-started/
  - https://vee-validate.logaretm.com/v4/guide/components/validation
---

# VeeValidate Recipes

## Setup form and field state

```vue
<script setup lang="ts">
import { useForm, useField } from 'vee-validate'
const { handleSubmit, errors, isSubmitting } = useForm({ initialValues: { email: '' } })
const { value: email } = useField<string>('email')
const submit = handleSubmit(async values => save(values))
</script>
<template>
  <form @submit="submit">
    <input v-model="email" type="email" />
    <span role="alert">{{ errors.email }}</span>
    <button :disabled="isSubmitting">Save</button>
  </form>
</template>
```

Use `handleSubmit` so validation runs before the callback; expose touched/errors to UI. Avoid duplicate field registration from both `<Field>` and `useField` for the same path.

## Validate a schema

Use `validationSchema` with supported schema adapter or field-level rules. Keep client validation for feedback and repeat authoritative validation on server.

## Field component

`<Form>`/`<Field>` components provide slot props for value, errors, meta and handlers. Bind input listeners carefully when using custom controls; ensure blur/change trigger policy matches UX.

## Dynamic fields and arrays

Use `useFieldArray` for repeatable nested fields and stable keys. Conditional unmount behavior affects whether values/errors are retained; choose `keepValue` policy intentionally.

## Server-side errors

Use `setErrors({ email: 'Already registered' })` or `setFieldError`; clear stale server errors after relevant edits and distinguish field errors from form-level failure.

## Read next

[[VeeValidate Form and Field Lifecycle]] · [[Vue API Recipes]] · [[Zod Recipes]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
