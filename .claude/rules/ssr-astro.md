# Astro

## Overview
Content-focused framework with Islands architecture

## Create Project

```bash
npm create astro@latest my-app
cd my-app
npm run dev
```

---

## Project Structure

```
src/
├── components/
│   ├── Button.astro
│   └── Card.astro
├── layouts/
│   └── Layout.astro
├── pages/
│   ├── index.astro     # /
│   ├── about.astro     # /about
│   └── blog/
│       ├── index.astro # /blog
│       └── [slug].astro # /blog/:slug
├── content/
│   └── blog/
│       └── post-1.md
└── styles/
    └── global.css
public/                 # Static files
astro.config.mjs
```

---

## Pages

```astro
---
// src/pages/index.astro
import Layout from '../layouts/Layout.astro';
import Card from '../components/Card.astro';

const pageTitle = 'Home';
const users = await fetch('https://api.example.com/users').then(r => r.json());
---

<Layout title={pageTitle}>
  <h1>Welcome</h1>
  {users.map((user) => (
    <Card name={user.name} />
  ))}
</Layout>
```

---

## Components

```astro
---
// src/components/Card.astro
interface Props {
  title: string;
  body?: string;
}

const { title, body } = Astro.props;
---

<div class="card">
  <h2>{title}</h2>
  {body && <p>{body}</p>}
  <slot />
</div>

<style>
  .card {
    padding: 1rem;
    border: 1px solid #ccc;
  }
</style>
```

---

## Layouts

```astro
---
// src/layouts/Layout.astro
interface Props {
  title: string;
}

const { title } = Astro.props;
---

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width" />
  <title>{title}</title>
</head>
<body>
  <header>
    <nav>
      <a href="/">Home</a>
      <a href="/about">About</a>
    </nav>
  </header>
  <main>
    <slot />
  </main>
</body>
</html>
```

---

## Islands (Client-side Components)

```astro
---
import ReactCounter from '../components/Counter.tsx';
import VueCounter from '../components/Counter.vue';
---

<!-- Load when visible -->
<ReactCounter client:visible />

<!-- Load on page load -->
<ReactCounter client:load />

<!-- Load when browser is idle -->
<ReactCounter client:idle />

<!-- Only on client (no SSR) -->
<ReactCounter client:only="react" />
```

---

## Content Collections

```ts
// src/content/config.ts
import { defineCollection, z } from 'astro:content';

const blog = defineCollection({
  schema: z.object({
    title: z.string(),
    date: z.date(),
    draft: z.boolean().default(false),
  }),
});

export const collections = { blog };
```

```astro
---
// src/pages/blog/[slug].astro
import { getCollection } from 'astro:content';

export async function getStaticPaths() {
  const posts = await getCollection('blog');
  return posts.map((post) => ({
    params: { slug: post.slug },
    props: { post },
  }));
}

const { post } = Astro.props;
const { Content } = await post.render();
---

<h1>{post.data.title}</h1>
<Content />
```

---

## Integrations

```bash
npx astro add tailwind
npx astro add react
npx astro add vue
npx astro add svelte
```

```js
// astro.config.mjs
import { defineConfig } from 'astro/config';
import tailwind from '@astrojs/tailwind';
import react from '@astrojs/react';

export default defineConfig({
  integrations: [tailwind(), react()],
});
```
