---
title: "FastAPI Dependency Injection and Lifetimes"
type: concept
domain: fastapi
level: intermediate
tags: [fastapi, python, dependency-injection]
status: researched
last_verified: 2026-11-20
sources:
  - https://fastapi.tiangolo.com/tutorial/dependencies/
---

# FastAPI Dependency Injection and Lifetimes

## Overview

Dependency system สร้าง dependency graph จาก endpoint parameters ให้แชร์ auth, db session, config และ resource cleanup โดยประกาศผ่าน type hints

## Mental model

`Depends` เรียก dependency ก่อน endpoint; ผลลัพธ์ cache ภายใน request โดย default เพื่อ reuse dependency เดียวกัน. `yield` dependency ทำ cleanup หลัง request/resource use. Async endpoint ควรไม่บล็อก event loop ด้วย blocking I/O; sync endpoint จะถูก run ใน threadpool ตาม framework behavior

## Example

```python
def get_session():
    session = SessionLocal()
    try:
        yield session
    finally:
        session.close()

@app.get('/users/{user_id}')
def read_user(user_id: int, session = Depends(get_session)):
    return session.get(User, user_id)
```

Snippet is a focused pattern; include package imports, types, error handling, validation and runtime configuration from the installed release before production use.

## Common mistakes and trade-offs

อย่าใช้ dependency cache เป็น global singleton; background tasks อาจมี lifecycle ต่างจาก request; ห้าม block event loop ใน async handler; dependency auth ต้องตรวจ object-level authorization ไม่ใช่แค่ login

## Practical guidance

แยก dependencies สำหรับ authentication, authorization, unit-of-work และ configuration; type return values; ทดสอบ override dependencies และ cancellation/cleanup

## Related knowledge

[[FastAPI]] · [[HTTP Request Lifecycle]] · [[OAuth Authorization Code with PKCE]] · [[Database-Transactions]] · [[Unit Integration and End-to-End Tests]]

## References

- [fastapi.tiangolo.com](https://fastapi.tiangolo.com/tutorial/dependencies/)
