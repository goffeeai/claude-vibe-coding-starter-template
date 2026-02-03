# SvelteKit

## Overview
Svelte framework with SSR, SSG, and file-based routing

## Create Project

```bash
npm create svelte@latest my-app
cd my-app
npm install
npm run dev
```

---

## Project Structure

```
src/
├── app.html            # HTML template
├── routes/
│   ├── +page.svelte    # /
│   ├── +layout.svelte  # Root layout
│   ├── about/
│   │   └── +page.svelte    # /about
│   └── blog/
│       ├── +page.svelte    # /blog
│       └── [slug]/
│           └── +page.svelte # /blog/:slug
├── lib/
│   └── components/
└── app.css
static/                 # Static files
svelte.config.js
```

---

## Pages

```svelte
<!-- src/routes/+page.svelte -->
<script lang="ts">
  export let data;
</script>

<h1>Welcome</h1>
<ul>
  {#each data.users as user}
    <li>{user.name}</li>
  {/each}
</ul>
```

---

## Data Loading

```ts
// src/routes/+page.server.ts
import type { PageServerLoad } from './$types';

export const load: PageServerLoad = async ({ fetch }) => {
  const response = await fetch('/api/users');
  const users = await response.json();

  return { users };
};
```

```svelte
<!-- src/routes/+page.svelte -->
<script lang="ts">
  import type { PageData } from './$types';
  export let data: PageData;
</script>

<h1>Users</h1>
{#each data.users as user}
  <p>{user.name}</p>
{/each}
```

---

## API Routes

```ts
// src/routes/api/users/+server.ts
import { json } from '@sveltejs/kit';
import type { RequestHandler } from './$types';

export const GET: RequestHandler = async () => {
  const users = await getUsers();
  return json(users);
};

export const POST: RequestHandler = async ({ request }) => {
  const body = await request.json();
  const user = await createUser(body);
  return json(user, { status: 201 });
};
```

---

## Layouts

```svelte
<!-- src/routes/+layout.svelte -->
<script>
  import '../app.css';
</script>

<header>
  <nav>
    <a href="/">Home</a>
    <a href="/about">About</a>
  </nav>
</header>

<main>
  <slot />
</main>
```

---

## Dynamic Routes

```svelte
<!-- src/routes/blog/[slug]/+page.svelte -->
<script lang="ts">
  import type { PageData } from './$types';
  export let data: PageData;
</script>

<h1>{data.post.title}</h1>
<article>{@html data.post.content}</article>
```

```ts
// src/routes/blog/[slug]/+page.server.ts
import type { PageServerLoad } from './$types';

export const load: PageServerLoad = async ({ params }) => {
  const post = await getPost(params.slug);
  return { post };
};
```

---

## Form Actions

```ts
// src/routes/login/+page.server.ts
import type { Actions } from './$types';

export const actions: Actions = {
  default: async ({ request }) => {
    const data = await request.formData();
    const email = data.get('email');
    const password = data.get('password');
    // Handle login
  }
};
```

```svelte
<form method="POST">
  <input name="email" type="email" />
  <input name="password" type="password" />
  <button type="submit">Login</button>
</form>
```
