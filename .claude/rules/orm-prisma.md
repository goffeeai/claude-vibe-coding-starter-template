# Prisma

## Overview
Modern TypeScript ORM with great DX

## Installation

```bash
npm install prisma @prisma/client
npx prisma init
```

---

## Schema (prisma/schema.prisma)

```prisma
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

generator client {
  provider = "prisma-client-js"
}

model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  name      String?
  posts     Post[]
  createdAt DateTime @default(now())
}

model Post {
  id        Int      @id @default(autoincrement())
  title     String
  content   String?
  published Boolean  @default(false)
  author    User     @relation(fields: [authorId], references: [id])
  authorId  Int
}
```

---

## Commands

```bash
npx prisma generate    # Generate client
npx prisma db push     # Push schema (dev)
npx prisma migrate dev # Create migration
npx prisma studio      # Open GUI
```

---

## CRUD Operations

```typescript
import { PrismaClient } from '@prisma/client';
const prisma = new PrismaClient();

// Create
const user = await prisma.user.create({
  data: { email: 'john@example.com', name: 'John' }
});

// Read
const users = await prisma.user.findMany();
const user = await prisma.user.findUnique({ where: { id: 1 } });
const user = await prisma.user.findFirst({ where: { email: { contains: 'john' } } });

// Update
const user = await prisma.user.update({
  where: { id: 1 },
  data: { name: 'Jane' }
});

// Delete
await prisma.user.delete({ where: { id: 1 } });
```

---

## Relations

```typescript
// Include relations
const userWithPosts = await prisma.user.findUnique({
  where: { id: 1 },
  include: { posts: true }
});

// Select specific fields
const user = await prisma.user.findUnique({
  where: { id: 1 },
  select: { name: true, email: true }
});

// Create with relation
const user = await prisma.user.create({
  data: {
    email: 'john@example.com',
    posts: {
      create: { title: 'First Post' }
    }
  }
});
```

---

## Filtering & Sorting

```typescript
const users = await prisma.user.findMany({
  where: {
    AND: [
      { email: { contains: '@gmail.com' } },
      { name: { not: null } }
    ]
  },
  orderBy: { createdAt: 'desc' },
  take: 10,
  skip: 0
});
```

---

## Best Practices

1. Use `prisma generate` after schema changes
2. Use transactions for multiple operations
3. Close connection in serverless: `prisma.$disconnect()`
