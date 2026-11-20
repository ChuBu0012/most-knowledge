---
title: React with TypeScript Recipes
type: reference
tags: [technical-knowledge, react, typescript, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://react.dev/learn/typescript
  - https://www.typescriptlang.org/docs/
---

# React with TypeScript Recipes

## Type props and children

```tsx
type PanelProps = { title: string; children: React.ReactNode; tone?: 'info' | 'warning' }
function Panel({ title, children, tone = 'info' }: PanelProps) {
  return <section data-tone={tone}><h2>{title}</h2>{children}</section>
}
```

Use `ReactNode` for renderable children; use narrow unions for variants rather than arbitrary strings.

## Type event handlers

```tsx
function SearchBox() {
  const [query, setQuery] = useState('')
  function onChange(event: React.ChangeEvent<HTMLInputElement>) {
    setQuery(event.currentTarget.value)
  }
  return <input value={query} onChange={onChange} />
}
```

Inline JSX handlers infer event type. Prefer inferred event types over manual casts.

## Type component callbacks

```tsx
type UserPickerProps = { onSelect: (user: User) => void }
```

Define callback contract in terms of domain data, not synthetic event, unless the parent specifically needs the DOM event.

## Type a reducer

```tsx
type State = { count: number }
type Action = { type: 'increment' } | { type: 'set'; value: number }
function reducer(state: State, action: Action): State {
  switch (action.type) {
    case 'increment': return { count: state.count + 1 }
    case 'set': return { count: action.value }
  }
}
```

Discriminated unions give safe exhaustiveness; avoid a broad string action type.

## Type refs

`useRef<HTMLInputElement>(null)` for DOM refs; `useRef<number | null>(null)` for mutable timer/instance handle. Refs do not cause rerender when changed.

## Read next

[[React Recipes]] · [[TypeScript Recipes]] · [[React TypeScript Props and Events]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
