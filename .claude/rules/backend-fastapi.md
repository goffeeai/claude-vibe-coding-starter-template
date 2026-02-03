# FastAPI

## Overview
Modern, fast Python web framework for building APIs

## Installation

```bash
pip install fastapi uvicorn[standard]
```

---

## Basic Server

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Hello World!"}

# Run: uvicorn main:app --reload
```

---

## Project Structure

```
app/
├── main.py           # Entry point
├── routers/
│   ├── __init__.py
│   └── users.py
├── models/
│   └── user.py
├── schemas/
│   └── user.py
├── services/
│   └── user_service.py
└── database.py
```

---

## Routing

```python
@app.get("/users")
def get_users():
    return users

@app.post("/users")
def create_user(user: UserCreate):
    return user

@app.get("/users/{user_id}")
def get_user(user_id: int):
    return {"user_id": user_id}
```

### Router (Modular)
```python
# routers/users.py
from fastapi import APIRouter

router = APIRouter(prefix="/users", tags=["users"])

@router.get("/")
def get_users():
    return []

# main.py
from routers import users
app.include_router(users.router)
```

---

## Pydantic Models (Schema)

```python
from pydantic import BaseModel, EmailStr
from typing import Optional

class UserCreate(BaseModel):
    name: str
    email: EmailStr
    age: Optional[int] = None

class UserResponse(BaseModel):
    id: int
    name: str
    email: str

    class Config:
        from_attributes = True
```

---

## Request & Response

```python
from fastapi import Query, Path, Body, Header

@app.get("/items")
def get_items(
    skip: int = Query(0, ge=0),
    limit: int = Query(10, le=100),
    token: str = Header(...)
):
    return {"skip": skip, "limit": limit}

@app.post("/users", response_model=UserResponse, status_code=201)
def create_user(user: UserCreate):
    return user
```

---

## Dependency Injection

```python
from fastapi import Depends

def get_db():
    db = Database()
    try:
        yield db
    finally:
        db.close()

@app.get("/users")
def get_users(db = Depends(get_db)):
    return db.query(User).all()
```

---

## Async Support

```python
@app.get("/users")
async def get_users():
    users = await fetch_users_from_db()
    return users
```

---

## API Documentation

FastAPI auto-generates docs:
- Swagger UI: `http://localhost:8000/docs`
- ReDoc: `http://localhost:8000/redoc`

---

## Running

```bash
# Development
uvicorn main:app --reload --port 8000

# Production
uvicorn main:app --host 0.0.0.0 --port 8000 --workers 4
```

---

## Why FastAPI?

- Fastest Python framework
- Auto validation with Pydantic
- Auto API documentation
- Async support
- Great for ML/AI backends
