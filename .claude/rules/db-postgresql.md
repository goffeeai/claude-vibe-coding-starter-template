# PostgreSQL

## Overview
Powerful open-source relational database

## Installation

### Local
```bash
# macOS
brew install postgresql
brew services start postgresql

# Ubuntu
sudo apt install postgresql postgresql-contrib
sudo systemctl start postgresql
```

### Docker
```bash
docker run --name postgres -e POSTGRES_PASSWORD=password -p 5432:5432 -d postgres
```

---

## Connection

### Connection String
```
postgresql://username:password@localhost:5432/database_name
```

### Node.js (pg)
```bash
npm install pg
```

```javascript
import pg from 'pg';
const { Pool } = pg;

const pool = new Pool({
  connectionString: process.env.DATABASE_URL
});

const result = await pool.query('SELECT * FROM users');
```

---

## Basic SQL

### Create Table
```sql
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  email VARCHAR(255) UNIQUE NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### CRUD
```sql
-- Create
INSERT INTO users (name, email) VALUES ('John', 'john@example.com');

-- Read
SELECT * FROM users;
SELECT * FROM users WHERE id = 1;

-- Update
UPDATE users SET name = 'Jane' WHERE id = 1;

-- Delete
DELETE FROM users WHERE id = 1;
```

---

## Data Types

| Type | Description |
|------|-------------|
| SERIAL | Auto-increment integer |
| INTEGER | Integer |
| VARCHAR(n) | Variable string |
| TEXT | Unlimited text |
| BOOLEAN | true/false |
| TIMESTAMP | Date and time |
| JSONB | JSON (binary) |
| UUID | Unique identifier |

---

## Indexes

```sql
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_name ON users(name);
```

---

## psql Commands

```bash
psql -U postgres                    # Connect
\l                                  # List databases
\c database_name                    # Connect to database
\dt                                 # List tables
\d table_name                       # Describe table
\q                                  # Quit
```

---

## GUI Tools

- **pgAdmin** - Official GUI
- **DBeaver** - Universal database tool
- **TablePlus** - Modern GUI (paid)
