---
title: Python Recipes
type: reference
domain: python
tags: [technical-knowledge, python, api-reference, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://docs.python.org/3/tutorial/
  - https://docs.python.org/3/library/
---

# Python Recipes

คู่มือค้นจากงานที่ต้องทำ ใช้ syntax ปัจจุบันของ Python 3; ตรวจ minimum version และ dependencies ในโปรเจกต์

## สร้าง virtual environment และติดตั้ง package

```sh
python3 -m venv .venv
source .venv/bin/activate       # Windows: .venv\\Scripts\\activate
python -m pip install fastapi uvicorn
python -m pip freeze > requirements.txt
```

แยก dependency ต่อโปรเจกต์เพื่อไม่ให้ชน global Python; production ควรใช้ lockfile/constraints ที่ทีมเลือก และ pin เวอร์ชันให้ทำซ้ำได้.

## ประกาศ function และ type hints

```python
from collections.abc import Sequence

def average(values: Sequence[float]) -> float:
    if not values:
        raise ValueError("values must not be empty")
    return sum(values) / len(values)
```

Type hints ช่วย editor, static checker และผู้อ่าน แต่ Python ไม่บังคับตรวจ type ตอน runtime. ใช้ `None`/exception ให้ชัดสำหรับ empty input.

## จัดข้อมูลด้วย dataclass

```python
from dataclasses import dataclass

@dataclass(frozen=True)
class User:
    id: str
    email: str
```

ใช้ `dataclass` กับข้อมูลที่มี field ชัด; `frozen=True` ป้องกัน assign field หลังสร้าง แต่ nested mutable values ยัง mutate ได้. อย่าใช้ dataclass แทนการ validate untrusted input.

## อ่าน/เขียนไฟล์อย่างปลอดภัย

```python
from pathlib import Path

path = Path("data/input.txt")
text = path.read_text(encoding="utf-8")
Path("data/output.txt").write_text(text.upper(), encoding="utf-8")
```

ใช้ `Path` แทนต่อ string path; ระบุ encoding; จัดการ `OSError` ตามกรณี. สำหรับไฟล์ใหญ่ให้เปิด stream แล้ววนทีละบรรทัดแทนโหลดทั้งไฟล์.

## จัดการ error

```python
try:
    value = int(raw)
except ValueError as exc:
    raise ValueError("count must be an integer") from exc
```

จับ exception ที่คาดว่าจะกู้คืนได้และแคบที่สุด; `raise ... from exc` รักษาสาเหตุ. อย่าจับ `Exception` แล้วคืนค่า default เงียบ ๆ.

## ใช้ comprehension / generator

```python
active_emails = [user.email.lower() for user in users if user.active]
large_rows = (parse(line) for line in file if line.strip())
```

list comprehension สร้าง list ใน memory; generator ประมวลทีละค่าและเหมาะกับ stream ขนาดใหญ่. เลือก loop ปกติเมื่อ comprehension ซ้อนจนอ่านยาก.

## ทำ HTTP API ด้วย FastAPI

```python
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel

app = FastAPI()
class ItemIn(BaseModel):
    name: str

@app.post("/items", status_code=201)
async def create_item(payload: ItemIn):
    if not payload.name.strip():
        raise HTTPException(422, "name is required")
    return {"id": "generated", "name": payload.name}
```

Pydantic model validate request payload; production handler ต้องใช้ persistence, auth, error mapping และ dependency boundaries จริง. รัน `uvicorn app:app --reload` สำหรับ dev เท่านั้น.

## ทำ async IO

```python
import asyncio

async def main():
    results = await asyncio.gather(fetch_one("a"), fetch_one("b"))
    return results

asyncio.run(main())
```

ใช้ async เมื่อ library ที่เรียกเป็น async และงานรอ IO; อย่าเรียก blocking CPU/IO โดยตรงใน event loop. จำกัด concurrency และตั้ง timeout เมื่อ fan-out ไป upstream.

## ค้นต่อ

[[FastAPI Dependency Injection and Lifetimes]] · [[Python]] · [[Unit Integration and End-to-End Tests]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
