---
title: "React TypeScript Props and Events"
type: concept
domain: react with typescript
level: intermediate
tags: [react, typescript, components]
status: researched
last_verified: 2026-11-20
sources:
  - https://react.dev/learn/typescript
---

# React TypeScript Props and Events

## Overview

กำหนด component contract ผ่าน props types และให้ DOM event types อนุมานจาก element ที่ใช้ ลดการ cast และทำให้ refactor ปลอดภัย

## Mental model

ใช้ `type`/`interface` สำหรับ props, discriminated unions สำหรับ mode ที่ mutually exclusive และ `ComponentPropsWithoutRef<"button">` เมื่อ wrapper ควรส่ง native button props ต่อ. Event handlers ควร infer จาก JSX (`onChange={event => ...}`); ref types ขึ้นกับ React major

## Example

```tsx
type Props =
  | { kind: 'link'; href: string; disabled?: never }
  | { kind: 'button'; onSave: () => void; disabled?: boolean };

function Action(props: Props) {
  if (props.kind === 'link') return <a href={props.href}>Open</a>;
  return <button disabled={props.disabled} onClick={props.onSave}>Save</button>;
}
```

Snippet is a focused pattern; include package imports, types, error handling, validation and runtime configuration from the installed release before production use.

## Common mistakes and trade-offs

`React.FC` ไม่จำเป็นสำหรับ component ปกติ; อย่าใส่ optional props ที่ผิด combination ได้; event object ต้องใช้ตาม callback ไม่ใช่เก็บไว้นอก lifecycle; runtime JSON ยังต้อง validate แม้ type ถูกต้อง

## Practical guidance

ใช้ API แบบ composition และ union ที่แทน state machine; public component ให้ type native DOM props อย่างระมัดระวัง ไม่เผย internal prop ที่พัง abstraction

## Related knowledge

[[React with TypeScript]] · [[TypeScript Type Narrowing]] · [[TypeScript Generics]] · [[React Component Composition]]

## References

- [react.dev](https://react.dev/learn/typescript)

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
