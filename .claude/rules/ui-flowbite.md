# Flowbite

## Overview
Tailwind CSS component library with JavaScript interactions

## Installation

```bash
npm install flowbite
```

```js
// tailwind.config.js
module.exports = {
  content: [
    './node_modules/flowbite/**/*.js'
  ],
  plugins: [
    require('flowbite/plugin')
  ]
}
```

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/flowbite/2.0.0/flowbite.min.js"></script>
```

---

## Components

### Button
```html
<button class="text-white bg-blue-700 hover:bg-blue-800 font-medium rounded-lg text-sm px-5 py-2.5">
  Default
</button>
```

### Modal
```html
<button data-modal-target="modal" data-modal-toggle="modal" class="btn">Open</button>

<div id="modal" class="hidden fixed inset-0 z-50 overflow-y-auto">
  <div class="relative p-4 w-full max-w-md">
    <div class="bg-white rounded-lg shadow">
      <div class="p-4 border-b">
        <h3>Modal Title</h3>
      </div>
      <div class="p-4">Content</div>
    </div>
  </div>
</div>
```

### Dropdown
```html
<button data-dropdown-toggle="dropdown" class="btn">Dropdown</button>
<div id="dropdown" class="hidden z-10 bg-white rounded shadow w-44">
  <ul class="py-2">
    <li><a href="#" class="block px-4 py-2 hover:bg-gray-100">Item 1</a></li>
    <li><a href="#" class="block px-4 py-2 hover:bg-gray-100">Item 2</a></li>
  </ul>
</div>
```

---

## Flowbite React

```bash
npm install flowbite-react
```

```tsx
import { Button, Modal, Card } from 'flowbite-react';

<Button>Click me</Button>
<Card>
  <h5>Card Title</h5>
  <p>Card content</p>
</Card>
```
