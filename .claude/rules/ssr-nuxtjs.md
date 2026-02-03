# Nuxt.js

## Overview
Vue framework with SSR, SSG, and file-based routing

## Create Project

```bash
npx nuxi@latest init my-app
cd my-app
npm install
npm run dev
```

---

## Project Structure

```
├── app.vue             # Root component
├── nuxt.config.ts      # Nuxt config
├── pages/
│   ├── index.vue       # /
│   ├── about.vue       # /about
│   └── blog/
│       ├── index.vue   # /blog
│       └── [slug].vue  # /blog/:slug
├── components/
│   └── Button.vue
├── composables/
│   └── useAuth.ts
├── server/
│   └── api/
│       └── users.ts    # /api/users
├── layouts/
│   └── default.vue
└── public/
```

---

## Pages

```vue
<!-- pages/index.vue -->
<script setup lang="ts">
const { data: users } = await useFetch('/api/users');
</script>

<template>
  <div>
    <h1>Users</h1>
    <ul>
      <li v-for="user in users" :key="user.id">
        {{ user.name }}
      </li>
    </ul>
  </div>
</template>
```

---

## Data Fetching

```vue
<script setup>
// Fetch data (SSR)
const { data, pending, error } = await useFetch('/api/users');

// With options
const { data } = await useFetch('/api/users', {
  key: 'users',
  lazy: false,
  server: true,
  transform: (data) => data.map(u => u.name)
});

// Async data
const { data } = await useAsyncData('users', () => {
  return $fetch('/api/users');
});
</script>
```

---

## API Routes

```ts
// server/api/users.ts
export default defineEventHandler(async (event) => {
  return [
    { id: 1, name: 'John' },
    { id: 2, name: 'Jane' }
  ];
});

// server/api/users/[id].ts
export default defineEventHandler(async (event) => {
  const id = getRouterParam(event, 'id');
  return { id, name: 'John' };
});

// POST with body
export default defineEventHandler(async (event) => {
  const body = await readBody(event);
  return { created: true, ...body };
});
```

---

## Composables

```ts
// composables/useAuth.ts
export const useAuth = () => {
  const user = useState<User | null>('user', () => null);

  async function login(email: string, password: string) {
    const data = await $fetch('/api/login', {
      method: 'POST',
      body: { email, password }
    });
    user.value = data.user;
  }

  async function logout() {
    await $fetch('/api/logout', { method: 'POST' });
    user.value = null;
  }

  return { user, login, logout };
};
```

---

## Layouts

```vue
<!-- layouts/default.vue -->
<template>
  <div>
    <header>
      <nav>
        <NuxtLink to="/">Home</NuxtLink>
        <NuxtLink to="/about">About</NuxtLink>
      </nav>
    </header>
    <main>
      <slot />
    </main>
  </div>
</template>
```

---

## SEO

```vue
<script setup>
useSeoMeta({
  title: 'My Page',
  description: 'Page description',
  ogTitle: 'My Page',
  ogDescription: 'Page description',
});

// Or useHead
useHead({
  title: 'My Page',
  meta: [
    { name: 'description', content: 'Page description' }
  ]
});
</script>
```

---

## nuxt.config.ts

```ts
export default defineNuxtConfig({
  devtools: { enabled: true },
  modules: ['@nuxtjs/tailwindcss', '@nuxt/ui'],
  css: ['~/assets/css/main.css'],
  runtimeConfig: {
    apiSecret: '',
    public: {
      apiBase: ''
    }
  }
});
```
