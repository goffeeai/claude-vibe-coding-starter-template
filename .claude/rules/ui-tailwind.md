# Tailwind CSS

## Overview
Utility-first CSS framework

## Installation

```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

---

## Configuration

```js
// tailwind.config.js
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx,vue,svelte}",
  ],
  theme: {
    extend: {
      colors: {
        primary: '#3490dc',
        secondary: '#ffed4a',
      },
      fontFamily: {
        sans: ['Inter', 'sans-serif'],
      },
    },
  },
  plugins: [],
}
```

---

## CSS Setup

```css
/* src/index.css */
@tailwind base;
@tailwind components;
@tailwind utilities;

/* Custom components */
@layer components {
  .btn {
    @apply px-4 py-2 rounded font-medium;
  }
  .btn-primary {
    @apply bg-blue-500 text-white hover:bg-blue-600;
  }
}
```

---

## Common Utilities

### Layout
```html
<div class="container mx-auto px-4">
<div class="flex items-center justify-between">
<div class="grid grid-cols-3 gap-4">
```

### Spacing
```html
<div class="p-4 m-2">      <!-- padding/margin -->
<div class="px-4 py-2">    <!-- horizontal/vertical -->
<div class="space-y-4">    <!-- gap between children -->
```

### Typography
```html
<h1 class="text-3xl font-bold">
<p class="text-gray-600 text-sm">
<span class="font-medium text-blue-500">
```

### Colors
```html
<div class="bg-blue-500 text-white">
<div class="border border-gray-300">
<div class="bg-gradient-to-r from-blue-500 to-purple-500">
```

### Responsive
```html
<div class="w-full md:w-1/2 lg:w-1/3">
<div class="hidden md:block">
<div class="text-sm md:text-base lg:text-lg">
```

### States
```html
<button class="hover:bg-blue-600 focus:ring-2 active:bg-blue-700">
<input class="focus:border-blue-500 focus:outline-none">
<div class="group-hover:visible">
```

---

## Components Examples

### Button
```html
<button class="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600 transition">
  Click me
</button>
```

### Card
```html
<div class="bg-white rounded-lg shadow-md p-6">
  <h3 class="text-xl font-semibold mb-2">Card Title</h3>
  <p class="text-gray-600">Card content here.</p>
</div>
```

### Input
```html
<input
  type="text"
  class="w-full px-3 py-2 border border-gray-300 rounded focus:outline-none focus:border-blue-500"
  placeholder="Enter text"
/>
```

### Navbar
```html
<nav class="bg-white shadow">
  <div class="container mx-auto px-4">
    <div class="flex items-center justify-between h-16">
      <a href="/" class="font-bold text-xl">Logo</a>
      <div class="flex space-x-4">
        <a href="/" class="text-gray-600 hover:text-gray-900">Home</a>
        <a href="/about" class="text-gray-600 hover:text-gray-900">About</a>
      </div>
    </div>
  </div>
</nav>
```

---

## Dark Mode

```js
// tailwind.config.js
export default {
  darkMode: 'class', // or 'media'
}
```

```html
<div class="bg-white dark:bg-gray-900 text-black dark:text-white">
```
