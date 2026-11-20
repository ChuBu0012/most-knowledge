---
title: TanStack Table Recipes
type: reference
tags: [technical-knowledge, tanstack-table, tables, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://tanstack.com/table/latest/docs/guide/introduction
---

# TanStack Table Recipes

Headless table: library builds row models/state; application renders accessible markup.

## Define columns and core row model

```tsx
const columns: ColumnDef<User>[] = [
  { accessorKey: 'name', header: 'Name' },
  { accessorKey: 'email', header: 'Email' },
]
const table = useReactTable({ data, columns, getCoreRowModel: getCoreRowModel() })
```

Keep `data` and `columns` stable (state/memo/module constant) to avoid unnecessary model recomputation. Use typed accessors for derived fields.

## Render header and cells

```tsx
<table>
 <thead>{table.getHeaderGroups().map(group => <tr key={group.id}>
  {group.headers.map(header => <th key={header.id} colSpan={header.colSpan}>
   {header.isPlaceholder ? null : flexRender(header.column.columnDef.header, header.getContext())}
  </th>)}
 </tr>)}</thead>
 <tbody>{table.getRowModel().rows.map(row => <tr key={row.id}>
  {row.getVisibleCells().map(cell => <td key={cell.id}>{flexRender(cell.column.columnDef.cell, cell.getContext())}</td>)}
 </tr>)}</tbody>
</table>
```

Preserve semantic table elements and accessible labels; handle empty/loading states outside row rendering.

## Add sorting/filter/pagination

Enable required state and row models: `getSortedRowModel`, `getFilteredRowModel`, `getPaginationRowModel`; wire `onSortingChange`/`state.sorting` to controlled React state when UI controls need it. For server-side data, set manual mode and send state to API rather than processing only the current page locally.

## Select rows

Enable row-selection state and stable `getRowId: row => row.id`; index IDs break when data sorts/pages. Verify keyboard interaction and bulk-action authorization.

## Read next

[[TanStack Table Row Models and Features]] · [[TanStack Virtual Recipes]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
