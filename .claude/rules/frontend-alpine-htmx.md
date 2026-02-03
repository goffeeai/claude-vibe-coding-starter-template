# Alpine.js + HTMX

## Overview
Lightweight alternatives for interactive HTML

---

## Alpine.js

### Installation
```html
<script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
```

### Basic Usage
```html
<div x-data="{ open: false, count: 0 }">
  <button @click="open = !open">Toggle</button>
  <div x-show="open">Content</div>

  <button @click="count++">Count: <span x-text="count"></span></button>
</div>
```

### Directives
```html
<!-- x-data: Define reactive data -->
<div x-data="{ name: 'John' }">

<!-- x-text: Set text content -->
<span x-text="name"></span>

<!-- x-html: Set HTML content -->
<div x-html="htmlContent"></div>

<!-- x-show: Toggle visibility -->
<div x-show="isVisible"></div>

<!-- x-if: Conditional rendering -->
<template x-if="isLoggedIn">
  <div>Welcome!</div>
</template>

<!-- x-for: Loop -->
<template x-for="item in items" :key="item.id">
  <li x-text="item.name"></li>
</template>

<!-- x-model: Two-way binding -->
<input x-model="name" />

<!-- x-bind: Bind attributes -->
<div x-bind:class="{ active: isActive }"></div>
<div :class="{ active: isActive }"></div>

<!-- @click: Event handling -->
<button @click="handleClick()">Click</button>
<button @click.prevent="handleSubmit()">Submit</button>
```

### Component Pattern
```html
<div x-data="dropdown()">
  <button @click="toggle()">Menu</button>
  <div x-show="open" @click.away="close()">
    <a href="#">Item 1</a>
    <a href="#">Item 2</a>
  </div>
</div>

<script>
  function dropdown() {
    return {
      open: false,
      toggle() { this.open = !this.open },
      close() { this.open = false }
    }
  }
</script>
```

---

## HTMX

### Installation
```html
<script src="https://unpkg.com/htmx.org@1.9.x"></script>
```

### Basic Usage
```html
<!-- GET request -->
<button hx-get="/api/users" hx-target="#result">
  Load Users
</button>
<div id="result"></div>

<!-- POST request -->
<form hx-post="/api/users" hx-target="#result">
  <input name="name" />
  <button type="submit">Create</button>
</form>

<!-- DELETE request -->
<button hx-delete="/api/users/1" hx-target="closest tr" hx-swap="outerHTML">
  Delete
</button>
```

### Attributes
```html
<!-- hx-get, hx-post, hx-put, hx-delete -->
<button hx-get="/api/data">GET</button>

<!-- hx-target: Where to put response -->
<button hx-get="/api/users" hx-target="#users-list">Load</button>

<!-- hx-swap: How to swap content -->
<button hx-get="/api/item" hx-swap="innerHTML">Replace inside</button>
<button hx-get="/api/item" hx-swap="outerHTML">Replace element</button>
<button hx-get="/api/item" hx-swap="beforeend">Append</button>
<button hx-get="/api/item" hx-swap="afterbegin">Prepend</button>

<!-- hx-trigger: When to trigger -->
<input hx-get="/search" hx-trigger="keyup changed delay:500ms" />
<div hx-get="/updates" hx-trigger="every 5s">Auto refresh</div>

<!-- hx-indicator: Loading indicator -->
<button hx-get="/api/data" hx-indicator="#spinner">
  Load
</button>
<div id="spinner" class="htmx-indicator">Loading...</div>
```

---

## Alpine + HTMX Together

```html
<div x-data="{ loading: false }">
  <button
    hx-get="/api/users"
    hx-target="#users"
    @htmx:before-request="loading = true"
    @htmx:after-request="loading = false"
  >
    <span x-show="!loading">Load Users</span>
    <span x-show="loading">Loading...</span>
  </button>

  <div id="users"></div>
</div>
```

---

## When to Use

### Alpine.js
- Simple interactivity (toggles, dropdowns)
- Form validation
- No build step needed

### HTMX
- Server-rendered HTML
- Progressive enhancement
- Partial page updates
