# Vue.js

## Overview
Progressive JavaScript framework

## Create Project

```bash
npm create vue@latest my-app
cd my-app
npm install
npm run dev
```

---

## Project Structure

```
src/
├── components/
│   ├── Button.vue
│   └── Card.vue
├── views/
│   ├── Home.vue
│   └── About.vue
├── composables/
│   └── useAuth.ts
├── stores/
│   └── auth.ts
├── router/
│   └── index.ts
├── App.vue
└── main.ts
```

---

## Components (Composition API)

```vue
<script setup lang="ts">
import { ref, computed } from 'vue';

interface Props {
  title: string;
  count?: number;
}

const props = withDefaults(defineProps<Props>(), {
  count: 0
});

const emit = defineEmits<{
  (e: 'update', value: number): void;
}>();

const localCount = ref(props.count);
const doubled = computed(() => localCount.value * 2);

function increment() {
  localCount.value++;
  emit('update', localCount.value);
}
</script>

<template>
  <div>
    <h1>{{ title }}</h1>
    <p>Count: {{ localCount }}</p>
    <p>Doubled: {{ doubled }}</p>
    <button @click="increment">Increment</button>
  </div>
</template>

<style scoped>
h1 {
  color: blue;
}
</style>
```

---

## Reactivity

```ts
import { ref, reactive, computed, watch } from 'vue';

// Ref (primitives)
const count = ref(0);
count.value++;

// Reactive (objects)
const user = reactive({
  name: 'John',
  email: 'john@example.com'
});
user.name = 'Jane';

// Computed
const fullName = computed(() => `${user.firstName} ${user.lastName}`);

// Watch
watch(count, (newVal, oldVal) => {
  console.log(`Count changed: ${oldVal} -> ${newVal}`);
});
```

---

## Composables

```ts
// composables/useAuth.ts
import { ref } from 'vue';

export function useAuth() {
  const user = ref<User | null>(null);
  const loading = ref(true);

  async function login(email: string, password: string) {
    // Login logic
  }

  async function logout() {
    // Logout logic
  }

  return { user, loading, login, logout };
}
```

---

## Pinia (State Management)

```ts
// stores/auth.ts
import { defineStore } from 'pinia';

export const useAuthStore = defineStore('auth', {
  state: () => ({
    user: null as User | null,
  }),
  getters: {
    isLoggedIn: (state) => !!state.user,
  },
  actions: {
    async login(email: string, password: string) {
      // Login logic
    },
  },
});
```

---

## Vue Router

```ts
// router/index.ts
import { createRouter, createWebHistory } from 'vue-router';

const router = createRouter({
  history: createWebHistory(),
  routes: [
    { path: '/', component: () => import('@/views/Home.vue') },
    { path: '/about', component: () => import('@/views/About.vue') },
    { path: '/users/:id', component: () => import('@/views/User.vue') },
  ],
});

export default router;
```
