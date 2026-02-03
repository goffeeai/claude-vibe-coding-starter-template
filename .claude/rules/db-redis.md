# Redis

## Overview
In-memory data store - great for caching and sessions

## Installation

### Docker
```bash
docker run --name redis -p 6379:6379 -d redis
```

---

## Connection

### Node.js (ioredis)
```bash
npm install ioredis
```

```javascript
import Redis from 'ioredis';
const redis = new Redis(process.env.REDIS_URL);

// String
await redis.set('key', 'value');
await redis.set('key', 'value', 'EX', 3600); // Expire in 1 hour
const value = await redis.get('key');

// Delete
await redis.del('key');
```

---

## Data Types

### String
```javascript
await redis.set('name', 'John');
await redis.get('name');
await redis.incr('counter');
```

### Hash
```javascript
await redis.hset('user:1', 'name', 'John', 'email', 'john@example.com');
await redis.hget('user:1', 'name');
await redis.hgetall('user:1');
```

### List
```javascript
await redis.lpush('queue', 'item1', 'item2');
await redis.rpop('queue');
await redis.lrange('queue', 0, -1);
```

### Set
```javascript
await redis.sadd('tags', 'node', 'redis');
await redis.smembers('tags');
await redis.sismember('tags', 'node');
```

---

## Common Use Cases

### Caching
```javascript
async function getUser(id) {
  const cached = await redis.get(`user:${id}`);
  if (cached) return JSON.parse(cached);

  const user = await db.findUser(id);
  await redis.set(`user:${id}`, JSON.stringify(user), 'EX', 3600);
  return user;
}
```

### Session Store
```javascript
// With express-session
import session from 'express-session';
import RedisStore from 'connect-redis';

app.use(session({
  store: new RedisStore({ client: redis }),
  secret: 'secret',
  resave: false,
  saveUninitialized: false
}));
```

### Rate Limiting
```javascript
async function rateLimit(ip) {
  const key = `rate:${ip}`;
  const count = await redis.incr(key);
  if (count === 1) await redis.expire(key, 60);
  return count <= 100;
}
```

---

## When to Use

- Caching
- Session storage
- Rate limiting
- Real-time leaderboards
- Pub/Sub messaging
- Job queues
