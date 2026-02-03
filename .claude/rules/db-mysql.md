# MySQL / MariaDB

## Overview
Popular open-source relational database

## Installation

### Docker
```bash
docker run --name mysql -e MYSQL_ROOT_PASSWORD=password -p 3306:3306 -d mysql
```

---

## Connection

### Connection String
```
mysql://username:password@localhost:3306/database_name
```

### Node.js (mysql2)
```bash
npm install mysql2
```

```javascript
import mysql from 'mysql2/promise';

const connection = await mysql.createConnection({
  host: 'localhost',
  user: 'root',
  password: 'password',
  database: 'mydb'
});

const [rows] = await connection.execute('SELECT * FROM users');
```

---

## Basic SQL

### Create Database & Table
```sql
CREATE DATABASE mydb;
USE mydb;

CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
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
| INT | Integer |
| VARCHAR(n) | Variable string |
| TEXT | Long text |
| BOOLEAN | TINYINT(1) |
| DATETIME | Date and time |
| JSON | JSON data |

---

## MySQL Commands

```bash
mysql -u root -p                    # Connect
SHOW DATABASES;                     # List databases
USE database_name;                  # Select database
SHOW TABLES;                        # List tables
DESCRIBE table_name;                # Describe table
EXIT;                               # Quit
```
