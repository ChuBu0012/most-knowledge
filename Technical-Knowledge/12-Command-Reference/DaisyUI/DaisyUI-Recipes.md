---
title: DaisyUI Recipes
type: reference
tags: [technical-knowledge, daisyui, tailwind, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://daisyui.com/docs/install/
  - https://daisyui.com/docs/themes/
---

# DaisyUI Recipes

## Install plugin (Tailwind v4)

```sh
npm install -D daisyui
```

```css
@import "tailwindcss";
@plugin "daisyui";
```

Confirm installation instructions for exact Tailwind/daisyUI major; v3 plugin configuration differs.

## Compose semantic components

```html
<button class="btn btn-primary">Save</button>
<div class="alert alert-warning"><span>Check the input</span></div>
<div class="card bg-base-100 shadow-xl"><div class="card-body">...</div></div>
```

Semantic component classes provide visual defaults; choose correct native element and accessible name/state. A styled `div` is not automatically a button/dialog.

## Select themes

Use `data-theme="light"` on root/container or configure available themes in plugin options. Theme variables define semantic colors such as `base-100`, `primary`, `neutral`; use them rather than hardcoding colors when a theme switch is expected.

## Combine with utilities

```html
<button class="btn btn-primary w-full sm:w-auto">Continue</button>
```

daisyUI component classes and Tailwind utilities can coexist. Resolve specificity by inspecting compiled styles; avoid accumulating contradictory utilities.

## Build an accessible dialog

Prefer native `<dialog>` with `showModal()` or a dedicated primitive for focus management, escape handling and inert background. daisyUI styles do not replace keyboard/focus behavior.

## Read next

[[Tailwind CSS Recipes]] · [[Utility-First CSS and Design Tokens]] · [[Reka UI Recipes]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
