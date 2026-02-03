# Hono

## Overview
Ultrafast web framework for the Edge

## Installation

```bash
npm install hono
```

---

## Basic Server

```typescript
import { Hono } from 'hono';
import { serve } from '@hono/node-server';

const app = new Hono();

app.get('/', (c) => {
  return c.json({ message: 'Hello Hono!' });
});

serve(app, (info) => {
  console.log(`Server running on port ${info.port}`);
});
```

---

## Routing

```typescript
app.get('/users', (c) => c.json(users));
app.post('/users', async (c) => {
  const body = await c.req.json();
  return c.json(body, 201);
});
app.get('/users/:id', (c) => {
  const id = c.req.param('id');
  return c.json({ id });
});
```

### Route Groups
```typescript
const api = new Hono();

api.get('/users', getUsers);
api.post('/users', createUser);

app.route('/api', api);
```

---

## Middleware

### Built-in
```typescript
import { cors } from 'hono/cors';
import { logger } from 'hono/logger';
import { prettyJSON } from 'hono/pretty-json';

app.use('*', logger());
app.use('*', cors());
app.use('*', prettyJSON());
```

### Custom
```typescript
app.use('*', async (c, next) => {
  console.log('Before');
  await next();
  console.log('After');
});
```

---

## Request & Context

```typescript
app.post('/users', async (c) => {
  // Request
  const body = await c.req.json();
  const query = c.req.query('name');
  const param = c.req.param('id');
  const header = c.req.header('Authorization');

  // Response
  return c.json({ data: body });
  // c.text('Hello');
  // c.html('<h1>Hello</h1>');
  // c.redirect('/login');
});
```

---

## Validation with Zod

```typescript
import { zValidator } from '@hono/zod-validator';
import { z } from 'zod';

const userSchema = z.object({
  name: z.string(),
  email: z.string().email(),
});

app.post('/users',
  zValidator('json', userSchema),
  (c) => {
    const user = c.req.valid('json');
    return c.json(user);
  }
);
```

---

## Deploy Targets

```typescript
// Node.js
import { serve } from '@hono/node-server';
serve(app);

// Bun
export default app;

// Cloudflare Workers
export default app;

// Deno
Deno.serve(app.fetch);
```

---

## Why Hono?

- Ultrafast (faster than Express)
- TypeScript native
- Works on Node, Bun, Deno, Cloudflare
- Tiny bundle size
- Modern API
