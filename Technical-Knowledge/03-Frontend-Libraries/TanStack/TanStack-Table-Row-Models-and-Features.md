---
title: "TanStack Table Row Models and Features"
type: concept
domain: tanstack table
level: intermediate
tags: [tanstack-table, data-grid]
status: researched
last_verified: 2026-11-20
sources:
  - https://tanstack.com/table/latest/docs/guide/row-models
---

# TanStack Table Row Models and Features

## Overview

TanStack Table แยก core row model ออกจาก feature row models เพื่อคำนวณ filter/sort/group/pagination โดยไม่กำหนด markup

## Mental model

แอปส่ง `data`, `columns`, controlled/uncontrolled state และ row-model factories; pipeline ประมวลผล core → filtered → sorted → grouped/expanded → paginated ตาม features ที่เปิด. Server-side pagination/filtering หมายถึงแอปส่ง state/query ไป API และตั้ง manual modes; client row model ไม่ได้เห็นข้อมูลทั้งชุด

## Example

```tsx
const table = useReactTable({
  data, columns,
  getCoreRowModel: getCoreRowModel(),
  getSortedRowModel: getSortedRowModel(),
  state: { sorting },
  onSortingChange: setSorting,
});
```

Snippet is a focused pattern; include package imports, types, error handling, validation and runtime configuration from the installed release before production use.

## Common mistakes and trade-offs

อย่าใช้ client sorting กับข้อมูลที่โหลดมาเพียง page เดียวแล้วคิดว่าเรียงทั้งฐานข้อมูล; columns/data reference churn ทำให้ recompute; virtualization ต้องรักษา accessibility/focus. Table v9 API แตกจาก v8

## Practical guidance

แยก server state/pagination จาก row-model feature; เลือกเฉพาะ features ที่ต้องใช้; test controlled state, sorting และ filter semantics; อ่าน migration v9 guide

## Related knowledge

[[TanStack-Table]] · [[TanStack Query Cache Lifecycle]] · [[List Virtualization and Windowing]] · [[HTTP Semantics and REST]]

## References

- [tanstack.com](https://tanstack.com/table/latest/docs/guide/row-models)

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
