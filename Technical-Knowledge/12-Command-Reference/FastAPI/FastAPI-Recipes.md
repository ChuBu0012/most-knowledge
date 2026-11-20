---
title: FastAPI Recipes
type: reference
tags: [technical-knowledge, fastapi, python, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://fastapi.tiangolo.com/tutorial/
  - https://fastapi.tiangolo.com/tutorial/dependencies/
---

# FastAPI Recipes

## Install and run

```sh
python -m pip install fastapi uvicorn
uvicorn app.main:app --reload
```

Use reload only in development. Pin Python and package versions for repeatable deploys.

## Declare request and response models

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()
class ItemIn(BaseModel):
    name: str
    price: float
class ItemOut(ItemIn):
    id: int

@app.post('/items', response_model=ItemOut, status_code=201)
async def create_item(item: ItemIn):
    return await repository.create(item)
```

Pydantic validates parsed input; response_model filters and documents output. Do not return ORM objects with secrets unless serialization policy excludes them.

## Path/query parameters

```python
@app.get('/items/{item_id}')
async def read_item(item_id: int, q: str | None = None):
    return await repository.find(item_id, q=q)
```

Type annotations drive validation/OpenAPI. Use explicit constraints where needed and return 404 for absent resources.

## Reuse auth/database via dependency

```python
from typing import Annotated
from fastapi import Depends, HTTPException
async def current_user(token: Annotated[str, Depends(oauth2_scheme)]):
    user = await verify_token(token)
    if user is None: raise HTTPException(401, 'invalid credentials')
    return user

@app.get('/me')
async def me(user: Annotated[User, Depends(current_user)]):
    return user
```

Dependencies form a request-scoped graph; use them for shared policy/resources. Keep authorization checks close to protected operations and consider dependency lifetime for streaming/background work.

## Handle known errors

```python
from fastapi import HTTPException
raise HTTPException(status_code=404, detail='item not found')
```

Use `HTTPException` for expected client-facing failure; register exception handlers for domain errors. Log unexpected errors server-side and avoid returning internal details.

## Background tasks and async

`BackgroundTasks` suits small best-effort work after response, not durable jobs. Use a queue for retryable/critical tasks. `async def` only helps when awaited IO clients are non-blocking; move CPU/blocking work to an appropriate worker.

## Test

```sh
python -m pip install httpx pytest
pytest
```

Use `TestClient` or async client with dependency overrides; isolate DB and external services. Test validation, auth, and error status codes.

## Read next

[[FastAPI Dependency Injection and Lifetimes]] · [[Python Recipes]] · [[OAuth Authorization Code with PKCE]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
