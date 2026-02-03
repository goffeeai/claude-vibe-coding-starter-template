# Express.js

## Overview
Minimal and flexible Node.js web framework

## Installation

```bash
npm install express
npm install -D @types/express  # TypeScript
```

---

## Basic Server

```javascript
import express from 'express';

const app = express();
const PORT = process.env.PORT || 3000;

// Middleware
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// Routes
app.get('/', (req, res) => {
  res.json({ message: 'Hello World!' });
});

app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

---

## Project Structure

```
src/
├── index.js          # Entry point
├── routes/
│   ├── index.js      # Route aggregator
│   ├── users.js
│   └── posts.js
├── controllers/
│   ├── userController.js
│   └── postController.js
├── middleware/
│   ├── auth.js
│   └── errorHandler.js
├── models/           # Database models
├── services/         # Business logic
└── utils/            # Utilities
```

---

## Routing

### Basic Routes
```javascript
app.get('/users', getUsers);
app.post('/users', createUser);
app.get('/users/:id', getUser);
app.put('/users/:id', updateUser);
app.delete('/users/:id', deleteUser);
```

### Router (Modular)
```javascript
// routes/users.js
import { Router } from 'express';
const router = Router();

router.get('/', getUsers);
router.post('/', createUser);
router.get('/:id', getUser);

export default router;

// index.js
import userRoutes from './routes/users.js';
app.use('/api/users', userRoutes);
```

---

## Middleware

### Built-in
```javascript
app.use(express.json());                    // Parse JSON
app.use(express.urlencoded({ extended: true })); // Parse form
app.use(express.static('public'));          // Static files
```

### Custom Middleware
```javascript
const logger = (req, res, next) => {
  console.log(`${req.method} ${req.path}`);
  next();
};

app.use(logger);
```

### Error Handler
```javascript
const errorHandler = (err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ error: 'Something went wrong!' });
};

app.use(errorHandler);  // Must be last
```

---

## Request & Response

```javascript
app.post('/users', (req, res) => {
  // Request
  const body = req.body;
  const query = req.query;      // ?name=john
  const params = req.params;    // /:id
  const headers = req.headers;

  // Response
  res.status(201).json({ user: body });
  // res.send('text');
  // res.redirect('/login');
});
```

---

## Common Middleware Packages

```bash
npm install cors helmet morgan cookie-parser
```

```javascript
import cors from 'cors';
import helmet from 'helmet';
import morgan from 'morgan';

app.use(cors());
app.use(helmet());
app.use(morgan('dev'));
```

---

## Express 5 Notes

- Use `{*splat}` for wildcard routes (not `*`)
- Async error handling built-in
