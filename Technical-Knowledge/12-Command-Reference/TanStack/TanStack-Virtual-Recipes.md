---
title: TanStack Virtual Recipes
type: reference
tags: [technical-knowledge, tanstack-virtual, performance, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://tanstack.com/virtual/latest/docs/introduction
---

# TanStack Virtual Recipes

## Virtualize a vertical list

```tsx
const parentRef = useRef<HTMLDivElement>(null)
const virtualizer = useVirtualizer({
  count: items.length,
  getScrollElement: () => parentRef.current,
  estimateSize: () => 36,
  getItemKey: index => items[index].id,
  overscan: 8,
})
```

Render a scroll container with fixed/known height, a spacer sized to `getTotalSize()`, and visible items positioned with `translateY(virtualItem.start)`. Use stable item keys; index keys can produce wrong row state after reorder.

## Variable row heights

Provide `measureElement` ref to each rendered item and a reasonable estimate. Fonts, images, and async content can change size; remeasure when layout changes. Overscan trades extra DOM for smoother scrolling.

## Virtualize table rows

Virtualize row model output while retaining real table semantics where possible. For extremely wide/complex layouts, use a grid with correct ARIA roles and keyboard navigation; virtualization alone does not make a table accessible.

## Know when not to virtualize

A few dozen rows often do not justify complexity. Virtualization reduces mounted DOM, not query cost, payload size, or sorting work. Combine with pagination/server filtering for very large datasets.

## Read next

[[List Virtualization and Windowing]] · [[TanStack Table Recipes]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
