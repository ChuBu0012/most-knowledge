---
title: Playwright Recipes
type: reference
tags: [technical-knowledge, playwright, e2e, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://playwright.dev/docs/intro
  - https://playwright.dev/docs/locators
---

# Playwright Recipes

## Install browsers and run

```sh
npm init playwright@latest
npx playwright install
npx playwright test
npx playwright test --ui
```

Pin Playwright package and browser binaries together in CI; install required system dependencies in runner image.

## Locate by accessible role

```ts
test('creates a task', async ({ page }) => {
  await page.goto('/tasks')
  await page.getByRole('textbox', { name: 'Task name' }).fill('Review API')
  await page.getByRole('button', { name: 'Add task' }).click()
  await expect(page.getByRole('listitem').filter({ hasText: 'Review API' })).toBeVisible()
})
```

Prefer role/name/label or explicit test ID for stable intent. Avoid brittle CSS selectors and arbitrary sleeps; locators auto-wait for actionability.

## Reuse authenticated state

Use a setup project to log in and save `storageState`; ensure state file is ignored by Git and contains no real user secrets. Use separate accounts/state per parallel worker when tests mutate shared data.

## Intercept network

`await page.route('**/api/**', route => route.fulfill({ json: fixture }))` isolates UI contract tests. Keep a smaller set of end-to-end tests against real backend to verify integration.

## Debug failure

Run `npx playwright test --trace on`; inspect trace/screenshots/video. Capture console/network errors where useful and remove nondeterministic dependencies rather than adding sleeps.

## Read next

[[Playwright Locators and Auto-Waiting]] · [[Vitest Recipes]] · [[Unit Integration and End-to-End Tests]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
