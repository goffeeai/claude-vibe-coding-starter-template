# SQLite

## Overview
Lightweight file-based database - perfect for small projects

## Installation

### Node.js (better-sqlite3)
```bash
npm install better-sqlite3
```

```javascript
import Database from 'better-sqlite3';
const db = new Database('myapp.db');

// Create table
db.exec(`
  CREATE TABLE IF NOT EXISTS users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    email TEXT UNIQUE
  )
`);

// Insert
const insert = db.prepare('INSERT INTO users (name, email) VALUES (?, ?)');
insert.run('John', 'john@example.com');

// Select
const users = db.prepare('SELECT * FROM users').all();
```

---

## Advantages

- No server needed (just a file)
- Zero configuration
- Great for development
- Perfect for small apps
- Portable (single file)

---

## When to Use

### ✅ Good for
- Small to medium apps
- Development/prototyping
- Single-user apps
- Embedded apps
- < 100K concurrent users

### ❌ Not ideal for
- High concurrency
- Multiple write operations
- Large scale apps

---

## Data Types

SQLite uses dynamic typing:
- NULL
- INTEGER
- REAL
- TEXT
- BLOB

---

## CLI

```bash
sqlite3 myapp.db              # Open database
.tables                       # List tables
.schema table_name            # Show schema
.quit                         # Exit
```
