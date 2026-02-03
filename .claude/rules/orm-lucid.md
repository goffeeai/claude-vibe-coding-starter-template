# Lucid ORM (AdonisJS)

## Overview
Active Record ORM for AdonisJS

## Installation

Comes with AdonisJS:
```bash
npm init adonisjs@latest my-app
# Select: API or Web application
```

---

## Model Definition

```typescript
// app/models/user.ts
import { DateTime } from 'luxon';
import { BaseModel, column, hasMany } from '@adonisjs/lucid/orm';
import Post from './post.js';

export default class User extends BaseModel {
  @column({ isPrimary: true })
  declare id: number;

  @column()
  declare email: string;

  @column()
  declare name: string | null;

  @column.dateTime({ autoCreate: true })
  declare createdAt: DateTime;

  @column.dateTime({ autoCreate: true, autoUpdate: true })
  declare updatedAt: DateTime;

  @hasMany(() => Post)
  declare posts: HasMany<typeof Post>;
}
```

---

## CRUD Operations

```typescript
import User from '#models/user';

// Create
const user = await User.create({
  email: 'john@example.com',
  name: 'John'
});

// Read
const users = await User.all();
const user = await User.find(1);
const user = await User.findOrFail(1);
const user = await User.findBy('email', 'john@example.com');

// Update
const user = await User.findOrFail(1);
user.name = 'Jane';
await user.save();

// or
await User.query().where('id', 1).update({ name: 'Jane' });

// Delete
const user = await User.findOrFail(1);
await user.delete();
```

---

## Query Builder

```typescript
// Basic query
const users = await User.query()
  .where('name', 'John')
  .orWhere('email', 'like', '%@gmail.com')
  .orderBy('created_at', 'desc')
  .limit(10);

// With relations
const user = await User.query()
  .where('id', 1)
  .preload('posts')
  .firstOrFail();
```

---

## Relations

```typescript
// app/models/post.ts
import { BaseModel, column, belongsTo } from '@adonisjs/lucid/orm';
import User from './user.js';

export default class Post extends BaseModel {
  @column({ isPrimary: true })
  declare id: number;

  @column()
  declare title: string;

  @column()
  declare userId: number;

  @belongsTo(() => User)
  declare user: BelongsTo<typeof User>;
}
```

### Relation Types
- `@hasOne` - One to One
- `@hasMany` - One to Many
- `@belongsTo` - Inverse One to One/Many
- `@manyToMany` - Many to Many

---

## Migrations

```bash
# Create migration
node ace make:migration users

# Run migrations
node ace migration:run

# Rollback
node ace migration:rollback
```

```typescript
// database/migrations/xxx_users.ts
import { BaseSchema } from '@adonisjs/lucid/schema';

export default class extends BaseSchema {
  protected tableName = 'users';

  async up() {
    this.schema.createTable(this.tableName, (table) => {
      table.increments('id');
      table.string('email').notNullable().unique();
      table.string('name').nullable();
      table.timestamp('created_at');
      table.timestamp('updated_at');
    });
  }

  async down() {
    this.schema.dropTable(this.tableName);
  }
}
```

---

## Seeders

```bash
node ace make:seeder user
node ace db:seed
```
