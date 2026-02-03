# SQLAlchemy (Python)

## Overview
The Python SQL toolkit and ORM

## Installation

```bash
pip install sqlalchemy
pip install psycopg2-binary  # PostgreSQL
```

---

## Setup

```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker, declarative_base

DATABASE_URL = "postgresql://user:pass@localhost/dbname"

engine = create_engine(DATABASE_URL)
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)
Base = declarative_base()
```

---

## Model Definition

```python
from sqlalchemy import Column, Integer, String, DateTime, ForeignKey
from sqlalchemy.orm import relationship
from datetime import datetime

class User(Base):
    __tablename__ = "users"

    id = Column(Integer, primary_key=True, index=True)
    email = Column(String, unique=True, index=True)
    name = Column(String, nullable=True)
    created_at = Column(DateTime, default=datetime.utcnow)

    posts = relationship("Post", back_populates="author")

class Post(Base):
    __tablename__ = "posts"

    id = Column(Integer, primary_key=True)
    title = Column(String)
    author_id = Column(Integer, ForeignKey("users.id"))

    author = relationship("User", back_populates="posts")
```

---

## CRUD Operations

```python
from sqlalchemy.orm import Session

# Create
def create_user(db: Session, email: str, name: str):
    user = User(email=email, name=name)
    db.add(user)
    db.commit()
    db.refresh(user)
    return user

# Read
def get_users(db: Session):
    return db.query(User).all()

def get_user(db: Session, user_id: int):
    return db.query(User).filter(User.id == user_id).first()

# Update
def update_user(db: Session, user_id: int, name: str):
    user = db.query(User).filter(User.id == user_id).first()
    user.name = name
    db.commit()
    return user

# Delete
def delete_user(db: Session, user_id: int):
    user = db.query(User).filter(User.id == user_id).first()
    db.delete(user)
    db.commit()
```

---

## With FastAPI

```python
from fastapi import Depends

def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()

@app.get("/users")
def read_users(db: Session = Depends(get_db)):
    return db.query(User).all()
```

---

## Queries

```python
# Filter
users = db.query(User).filter(User.name == "John").all()
users = db.query(User).filter(User.email.like("%@gmail.com")).all()

# Order
users = db.query(User).order_by(User.created_at.desc()).all()

# Limit
users = db.query(User).limit(10).offset(0).all()

# Join
results = db.query(User).join(Post).all()
```

---

## Migrations (Alembic)

```bash
pip install alembic
alembic init alembic
alembic revision --autogenerate -m "Create users table"
alembic upgrade head
```
