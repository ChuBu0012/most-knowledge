---
title: Reka UI Recipes
type: reference
tags: [technical-knowledge, reka-ui, vue, accessibility, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://reka-ui.com/docs/overview/introduction
  - https://reka-ui.com/docs/components/dialog
---

# Reka UI Recipes

Reka UI provides unstyled Vue primitives. It manages interaction/accessibility mechanics; you provide visual styles.

## Install

```sh
npm install reka-ui
```

Import primitives from component entry points documented for installed version. Keep package version aligned with Vue 3 requirements.

## Build a dialog

```vue
<script setup lang="ts">
import { DialogRoot, DialogTrigger, DialogPortal, DialogOverlay, DialogContent, DialogTitle, DialogClose } from 'reka-ui'
</script>
<template>
  <DialogRoot>
    <DialogTrigger>Open settings</DialogTrigger>
    <DialogPortal>
      <DialogOverlay class="overlay" />
      <DialogContent aria-describedby="settings-help">
        <DialogTitle>Settings</DialogTitle>
        <p id="settings-help">Choose preferences.</p>
        <DialogClose>Close</DialogClose>
      </DialogContent>
    </DialogPortal>
  </DialogRoot>
</template>
```

Primitive handles focus/keyboard semantics; style overlay/content and verify focus returns to trigger. Keep title and accessible description connected.

## Controlled open state

Use `v-model:open="open"` on the root when application state controls visibility; use uncontrolled `defaultOpen` for local trigger-only behavior. Avoid multiple competing owners of open state.

## Compose select/menu

Use Root/Trigger/Portal/Content/Item primitives and stable values. Preserve keyboard navigation and roles; do not replace built-in semantics with clickable generic elements without a reason.

## Style state

Use data attributes/state slots supplied by component to style open/checked/disabled states. Test keyboard-only navigation, escape/outside dismissal, reduced motion and high contrast.

## Read next

[[Vue API Recipes]] · [[DaisyUI Recipes]] · [[Reka UI]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
