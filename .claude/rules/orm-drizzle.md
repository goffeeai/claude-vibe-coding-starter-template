# Drizzle ORM

## Overview
Lightweight TypeScript ORM - SQL-like syntax

## Installation

```bash
npm install drizzle-orm
npm install -D drizzle-kit
```

### For PostgreSQL
```bash
npm install pg
```

### For MySQL
```bash
npm install mysql2
```

---

## Schema Definition

```typescript
// src/db/schema.ts
import { pgTable, serial, text, timestamp, integer } from 'drizzle-orm/pg-core';

export const users = pgTable('users', {
  id: serial('id').primaryKey(),
  name: text('name').notNull(),
  email: text('email').unique().notNull(),
  createdAt: timestamp('created_at').defaultNow()
});

export const posts = pgTable('posts', {
  id: serial('id').primaryKey(),
  title: text('title').notNull(),
  content: text('content'),
  authorId: integer('author_id').references(() => users.id)
});
```

---

## Database Connection

```typescript
// src/db/index.ts
import { drizzle } from 'drizzle-orm/node-postgres';
import { Pool } from 'pg';
import * as schema from './schema';

const pool = new Pool({
  connectionString: process.env.DATABASE_URL
});

export const db = drizzle(pool, { schema });
```

---

## CRUD Operations

```typescript
import { db } from './db';
import { users, posts } from './db/schema';
import { eq, and, like } from 'drizzle-orm';

// Create
const user = await db.insert(users)
  .values({ name: 'John', email: 'john@example.com' })
  .returning();

// Read
const allUsers = await db.select().from(users);
const oneUser = await db.select().from(users).where(eq(users.id, 1));

// Update
await db.update(users)
  .set({ name: 'Jane' })
  .where(eq(users.id, 1));

// Delete
await db.delete(users).where(eq(users.id, 1));
```

---

## Queries

```typescript
// With filter
const result = await db.select()
  .from(users)
  .where(and(
    like(users.email, '%@gmail.com'),
    eq(users.name, 'John')
  ));

// With join
const result = await db.select()
  .from(users)
  .leftJoin(posts, eq(users.id, posts.authorId));

// With limit and offset
const result = await db.select()
  .from(users)
  .limit(10)
  .offset(0);
```

---

## Migrations

```typescript
// drizzle.config.ts
export default {
  schema: './src/db/schema.ts',
  out: './drizzle',
  driver: 'pg',
  dbCredentials: {
    connectionString: process.env.DATABASE_URL!
  }
};
```

```bash
npx drizzle-kit generate:pg  # Generate migration
npx drizzle-kit push:pg      # Push to database
npx drizzle-kit studio       # Open GUI
```

---

## Why Drizzle?

- SQL-like syntax
- Lightweight (no code generation)
- Great TypeScript support
- Fast
