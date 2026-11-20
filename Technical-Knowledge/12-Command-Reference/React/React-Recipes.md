---
title: "React Recipes"
type: reference
domain: react
tags: [technical-knowledge, api-reference, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://react.dev/reference/react
---

# React Recipes

คู่มือค้นจากงานที่ต้องทำ ตัวอย่างมุ่งที่ API/คำสั่งที่ใช้บ่อย; ตรวจ runtime/compiler version ในโปรเจกต์ก่อนใช้

## สร้าง component และแสดงรายการ

```tsx
type User = { id: string; name: string };
function UserList({ users }: { users: User[] }) {
  return <ul>{users.map(user => <li key={user.id}>{user.name}</li>)}</ul>;
}
```

ใช้ stable key จากข้อมูล; key ใช้ให้ React รักษา component identity ไม่ใช่ prop ที่อ่านได้ใน child.

## เก็บ state ด้วย `useState`

```tsx
const [count, setCount] = useState(0);
setCount(current => current + 1);
```

ใช้ updater form เมื่อค่าถัดไปขึ้นกับค่าปัจจุบันหรือมีหลาย update ใน event เดียว. อย่า mutate object/array state; สร้างค่าใหม่.

## รับ input form

```tsx
const [email, setEmail] = useState('');
<input value={email} onChange={event => setEmail(event.currentTarget.value)} />
```

Controlled input ต้องอัปเดต state ใน onChange ทุกครั้ง; input ที่ไม่ต้อง sync ทุก keystroke ใช้ uncontrolled/ref หรือ form library.

## เชื่อมระบบภายนอกด้วย `useEffect`

```tsx
useEffect(() => {
  const connection = createConnection(roomId);
  connection.connect();
  return () => connection.disconnect();
}, [roomId]);
```

Effect ใช้ synchronize กับ subscription/browser API/widget; cleanup ก่อน re-run และ unmount. อย่าใช้ effect คำนวณ derived state หรือจัดการ event ที่ควรทำใน handler.

## โหลดข้อมูลและยกเลิก request

```tsx
useEffect(() => {
  const controller = new AbortController();
  fetch(`/api/users/${userId}`, { signal: controller.signal })
    .then(r => { if (!r.ok) throw new Error(`HTTP ${r.status}`); return r.json(); })
    .then(setUser).catch(error => { if (!controller.signal.aborted) setError(error); });
  return () => controller.abort();
}, [userId]);
```

สำหรับ caching, dedupe, retry, invalidation ใช้ server-state tool อย่าง [[TanStack Query]]; effect แบบนี้เหมาะกับตัวอย่างเล็กและระบบภายนอก.

## แชร์ state ผ่าน context

```tsx
const ThemeContext = createContext<'light' | 'dark' | null>(null);
function useTheme() {
  const value = useContext(ThemeContext);
  if (value === null) throw new Error('ThemeProvider missing');
  return value;
}
```

Context เหมาะกับค่าที่ subtree ใช้ร่วมกัน เช่น theme/locale; การเปลี่ยน provider value ทำให้ consumers render. State ที่เปลี่ยนถี่มากอาจแยก context หรือใช้ store selector.

## ใช้ ref กับ DOM

```tsx
const inputRef = useRef<HTMLInputElement>(null);
return <input ref={inputRef} />;
// event handler: inputRef.current?.focus()
```

ใช้ ref สำหรับ imperative API (focus, measurement, third-party instance) ไม่ใช่เก็บค่าที่ต้องแสดงผล เพราะ ref เปลี่ยนแล้วไม่ trigger render.

## ลด render ที่แพงอย่างมีหลักฐาน

`memo(Component)`, `useMemo(() => expensive(data), [data])`, `useCallback(fn, [deps])` เป็น optimization ไม่ใช่ข้อบังคับ. วัดด้วย Profiler ก่อน; props/state/context ที่เปลี่ยนยังทำให้ component render ได้.

## ค้นต่อ

[[React Rendering Model]] · [[React State and Batching]] · [[React Effect Synchronization]] · [[React Component Identity and Keys]] · [[React Server and Client Components]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
