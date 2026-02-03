# TypeORM

## Overview
ORM for TypeScript with decorators

## Installation

```bash
npm install typeorm reflect-metadata
npm install pg  # or mysql2, sqlite3, etc.
```

---

## Configuration

```typescript
// data-source.ts
import { DataSource } from 'typeorm';

export const AppDataSource = new DataSource({
  type: 'postgres',
  url: process.env.DATABASE_URL,
  entities: ['src/entity/**/*.ts'],
  migrations: ['src/migration/**/*.ts'],
  synchronize: false, // Don't use in production!
});

// Initialize
await AppDataSource.initialize();
```

---

## Entity Definition

```typescript
// src/entity/User.ts
import { Entity, PrimaryGeneratedColumn, Column, OneToMany, CreateDateColumn } from 'typeorm';
import { Post } from './Post';

@Entity()
export class User {
  @PrimaryGeneratedColumn()
  id: number;

  @Column({ unique: true })
  email: string;

  @Column({ nullable: true })
  name: string;

  @CreateDateColumn()
  createdAt: Date;

  @OneToMany(() => Post, (post) => post.author)
  posts: Post[];
}
```

---

## CRUD Operations

```typescript
import { AppDataSource } from './data-source';
import { User } from './entity/User';

const userRepository = AppDataSource.getRepository(User);

// Create
const user = userRepository.create({
  email: 'john@example.com',
  name: 'John'
});
await userRepository.save(user);

// Read
const users = await userRepository.find();
const user = await userRepository.findOneBy({ id: 1 });
const user = await userRepository.findOne({
  where: { id: 1 },
  relations: ['posts']
});

// Update
await userRepository.update(1, { name: 'Jane' });

// Delete
await userRepository.delete(1);
```

---

## Query Builder

```typescript
const users = await userRepository
  .createQueryBuilder('user')
  .where('user.email LIKE :email', { email: '%@gmail.com' })
  .orderBy('user.createdAt', 'DESC')
  .getMany();
```

---

## Relations

```typescript
// @OneToOne
@OneToOne(() => Profile)
@JoinColumn()
profile: Profile;

// @OneToMany
@OneToMany(() => Post, (post) => post.author)
posts: Post[];

// @ManyToOne
@ManyToOne(() => User, (user) => user.posts)
author: User;

// @ManyToMany
@ManyToMany(() => Tag)
@JoinTable()
tags: Tag[];
```

---

## Migrations

```bash
# Generate migration
npx typeorm migration:generate -d src/data-source.ts src/migration/CreateUsers

# Run migrations
npx typeorm migration:run -d src/data-source.ts

# Revert
npx typeorm migration:revert -d src/data-source.ts
```
