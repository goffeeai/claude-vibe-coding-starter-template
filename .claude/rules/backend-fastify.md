# Fastify

## Overview
Fast and low overhead web framework for Node.js

## Installation

```bash
npm install fastify
```

---

## Basic Server

```javascript
import Fastify from 'fastify';

const fastify = Fastify({ logger: true });

fastify.get('/', async (request, reply) => {
  return { message: 'Hello World!' };
});

const start = async () => {
  try {
    await fastify.listen({ port: 3000, host: '0.0.0.0' });
  } catch (err) {
    fastify.log.error(err);
    process.exit(1);
  }
};

start();
```

---

## Project Structure

```
src/
├── index.js
├── routes/
│   ├── index.js
│   └── users.js
├── plugins/
│   ├── auth.js
│   └── database.js
├── schemas/
│   └── user.js
└── services/
```

---

## Routing

### Basic Routes
```javascript
fastify.get('/users', getUsers);
fastify.post('/users', createUser);
fastify.get('/users/:id', getUser);
```

### Route with Schema Validation
```javascript
const userSchema = {
  body: {
    type: 'object',
    required: ['name', 'email'],
    properties: {
      name: { type: 'string' },
      email: { type: 'string', format: 'email' }
    }
  },
  response: {
    200: {
      type: 'object',
      properties: {
        id: { type: 'integer' },
        name: { type: 'string' }
      }
    }
  }
};

fastify.post('/users', { schema: userSchema }, createUser);
```

---

## Plugins

### Register Plugin
```javascript
// plugins/database.js
async function dbPlugin(fastify, options) {
  fastify.decorate('db', yourDbConnection);
}

export default dbPlugin;

// index.js
import dbPlugin from './plugins/database.js';
fastify.register(dbPlugin);
```

### Common Plugins
```bash
npm install @fastify/cors @fastify/helmet @fastify/cookie
```

```javascript
import cors from '@fastify/cors';
import helmet from '@fastify/helmet';

await fastify.register(cors);
await fastify.register(helmet);
```

---

## Request & Reply

```javascript
fastify.post('/users', async (request, reply) => {
  const body = request.body;
  const query = request.query;
  const params = request.params;
  const headers = request.headers;

  // Reply
  return { user: body };  // Auto JSON
  // reply.code(201).send({ user: body });
});
```

---

## Error Handling

```javascript
fastify.setErrorHandler((error, request, reply) => {
  fastify.log.error(error);
  reply.status(500).send({ error: 'Something went wrong' });
});
```

---

## TypeScript

```typescript
import Fastify, { FastifyRequest, FastifyReply } from 'fastify';

interface UserBody {
  name: string;
  email: string;
}

fastify.post<{ Body: UserBody }>('/users', async (request, reply) => {
  const { name, email } = request.body;
  return { name, email };
});
```

---

## Why Fastify?

- 2x faster than Express
- Built-in schema validation
- TypeScript support
- Plugin system
- Logging built-in
