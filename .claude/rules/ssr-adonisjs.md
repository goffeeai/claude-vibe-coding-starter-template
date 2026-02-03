# AdonisJS

## Overview
Full-stack Node.js framework with SSR via Edge.js

## Create Project

```bash
npm init adonisjs@latest my-app
# Select: Web application (with server rendered views)
cd my-app
npm run dev
```

---

## Project Structure

```
├── app/
│   ├── controllers/
│   │   └── HomeController.ts
│   ├── models/
│   │   └── User.ts
│   ├── middleware/
│   └── validators/
├── config/
├── database/
│   └── migrations/
├── resources/
│   └── views/
│       ├── layouts/
│       │   └── main.edge
│       └── pages/
│           └── home.edge
├── start/
│   ├── routes.ts
│   └── kernel.ts
└── public/
```

---

## Routes

```ts
// start/routes.ts
import router from '@adonisjs/core/services/router';
const HomeController = () => import('#controllers/HomeController');
const UsersController = () => import('#controllers/UsersController');

router.get('/', [HomeController, 'index']);
router.get('/about', [HomeController, 'about']);

// Resource routes
router.resource('users', UsersController);

// API routes
router.group(() => {
  router.get('/users', [UsersController, 'index']);
  router.post('/users', [UsersController, 'store']);
}).prefix('api');
```

---

## Controllers

```ts
// app/controllers/HomeController.ts
import type { HttpContext } from '@adonisjs/core/http';

export default class HomeController {
  async index({ view }: HttpContext) {
    const users = await User.all();
    return view.render('pages/home', { users });
  }

  async about({ view }: HttpContext) {
    return view.render('pages/about');
  }
}
```

---

## Edge Templates (Views)

```edge
{{-- resources/views/layouts/main.edge --}}
<!DOCTYPE html>
<html>
<head>
  <title>{{ title ?? 'My App' }}</title>
  @vite(['resources/css/app.css', 'resources/js/app.js'])
</head>
<body>
  <header>
    <nav>
      <a href="/">Home</a>
      <a href="/about">About</a>
    </nav>
  </header>
  <main>
    @!section('content')
  </main>
</body>
</html>
```

```edge
{{-- resources/views/pages/home.edge --}}
@layout('layouts/main')
@set('title', 'Home')

@section('content')
  <h1>Welcome</h1>

  @each(user in users)
    <div class="card">
      <h2>{{ user.name }}</h2>
      <p>{{ user.email }}</p>
    </div>
  @endeach

  @if(users.length === 0)
    <p>No users found</p>
  @endif
@endsection
```

---

## Models

```ts
// app/models/User.ts
import { DateTime } from 'luxon';
import { BaseModel, column, hasMany } from '@adonisjs/lucid/orm';

export default class User extends BaseModel {
  @column({ isPrimary: true })
  declare id: number;

  @column()
  declare email: string;

  @column()
  declare name: string;

  @column.dateTime({ autoCreate: true })
  declare createdAt: DateTime;
}
```

---

## Validation

```ts
// app/validators/UserValidator.ts
import vine from '@vinejs/vine';

export const createUserValidator = vine.compile(
  vine.object({
    name: vine.string().minLength(2),
    email: vine.string().email().unique({ table: 'users', column: 'email' }),
    password: vine.string().minLength(8),
  })
);

// In controller
const data = await request.validateUsing(createUserValidator);
```

---

## Vite Integration

```ts
// vite.config.ts
import { defineConfig } from 'vite';
import adonisjs from '@adonisjs/vite/client';

export default defineConfig({
  plugins: [
    adonisjs({
      entrypoints: ['resources/css/app.css', 'resources/js/app.js'],
    }),
  ],
});
```

---

## CLI Commands

```bash
node ace make:controller User    # Create controller
node ace make:model User -m      # Create model + migration
node ace make:migration users    # Create migration
node ace migration:run           # Run migrations
node ace make:validator User     # Create validator
```
