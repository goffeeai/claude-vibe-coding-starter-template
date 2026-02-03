# Svelte

## Overview
Compile-time framework - no virtual DOM

## Create Project

```bash
npm create svelte@latest my-app
cd my-app
npm install
npm run dev
```

---

## Component Basics

```svelte
<script lang="ts">
  // Props
  export let name: string;
  export let count = 0;

  // Reactive
  let message = 'Hello';

  // Derived
  $: doubled = count * 2;

  // Function
  function increment() {
    count++;
  }
</script>

<h1>{message}, {name}!</h1>
<p>Count: {count}</p>
<p>Doubled: {doubled}</p>
<button on:click={increment}>Click me</button>

<style>
  h1 {
    color: blue;
  }
</style>
```

---

## Reactivity

```svelte
<script>
  let count = 0;

  // Reactive statement
  $: doubled = count * 2;

  // Reactive block
  $: {
    console.log('count is', count);
    console.log('doubled is', doubled);
  }

  // Reactive if
  $: if (count > 10) {
    alert('count is too high!');
  }
</script>
```

---

## Events

```svelte
<script>
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  function handleClick() {
    dispatch('message', { text: 'Hello!' });
  }
</script>

<!-- Event handling -->
<button on:click={handleClick}>Click</button>
<input on:input={(e) => console.log(e.target.value)} />

<!-- Event modifiers -->
<button on:click|once={handleClick}>Once</button>
<form on:submit|preventDefault={handleSubmit}>
```

---

## Bindings

```svelte
<script>
  let name = '';
  let checked = false;
  let selected = '';
</script>

<input bind:value={name} />
<input type="checkbox" bind:checked />
<select bind:value={selected}>
  <option value="a">A</option>
  <option value="b">B</option>
</select>
```

---

## Stores

```ts
// stores.ts
import { writable, derived, readable } from 'svelte/store';

export const count = writable(0);
export const doubled = derived(count, ($count) => $count * 2);

// Usage in component
import { count, doubled } from './stores';

// Auto-subscribe with $
<p>Count: {$count}</p>
<p>Doubled: {$doubled}</p>
<button on:click={() => $count++}>+</button>
```

---

## Each & If

```svelte
{#each items as item, i (item.id)}
  <li>{i}: {item.name}</li>
{:else}
  <li>No items</li>
{/each}

{#if user}
  <p>Welcome, {user.name}</p>
{:else if loading}
  <p>Loading...</p>
{:else}
  <p>Please log in</p>
{/if}
```
