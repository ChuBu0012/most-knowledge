---
title: Tailwind CSS Recipes
type: reference
tags: [technical-knowledge, tailwind, css, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://tailwindcss.com/docs/installation
  - https://tailwindcss.com/docs/styling-with-utility-classes
---

# Tailwind CSS Recipes

Examples target Tailwind CSS v4. Do not mix v3 config/plugin instructions with v4 CSS-first setup.

## Install with Vite

```sh
npm install tailwindcss @tailwindcss/vite
```

Add `tailwindcss()` to Vite plugins and import Tailwind in CSS:

```css
@import "tailwindcss";
```

## Style layout and states

```html
<main class="mx-auto flex max-w-5xl flex-col gap-6 px-4 py-8 md:flex-row">
  <button class="rounded-md bg-blue-600 px-4 py-2 text-white hover:bg-blue-700 focus-visible:outline-2 disabled:opacity-50">
    Save
  </button>
</main>
```

Compose utilities for layout, spacing, typography and states. Use semantic HTML and visible focus styles; utility classes do not provide accessibility automatically.

## Define design tokens/theme

```css
@import "tailwindcss";
@theme {
  --color-brand-600: oklch(0.52 0.18 255);
  --font-display: "Inter", sans-serif;
  --breakpoint-3xl: 120rem;
}
```

Use named tokens for repeated values. Keep contrast and responsive behavior in mind when changing color scales.

## Conditional classes

Use framework expressions to select complete class strings, e.g. `isActive ? 'bg-blue-700 text-white' : 'bg-white text-slate-900'`. Avoid constructing class names from fragments that the scanner cannot detect (`bg-${color}-500`); map finite variants to literal class sets.

## Extract repeated patterns

Prefer component abstractions for repeated semantic UI. Use `@apply` sparingly when CSS belongs to a selector; excessive `@apply` recreates an opaque CSS layer and obscures component boundaries.

## Responsive and dark mode

Use mobile-first variants such as `md:grid-cols-2`; dark mode via configured strategy/variant. Test actual narrow and wide layouts plus keyboard/focus states.

## Read next

[[Utility-First CSS and Design Tokens]] · [[DaisyUI Recipes]] · [[Reka UI Recipes]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
