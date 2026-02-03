# DaisyUI

## Overview
Tailwind CSS component library with beautiful defaults

## Installation

```bash
npm install -D daisyui@latest
```

```js
// tailwind.config.js
export default {
  plugins: [require("daisyui")],
  daisyui: {
    themes: ["light", "dark", "cupcake"],
  },
}
```

---

## Themes

```html
<!-- Set theme on html -->
<html data-theme="light">

<!-- Or dark -->
<html data-theme="dark">
```

---

## Components

### Button
```html
<button class="btn">Default</button>
<button class="btn btn-primary">Primary</button>
<button class="btn btn-secondary">Secondary</button>
<button class="btn btn-accent">Accent</button>
<button class="btn btn-ghost">Ghost</button>
<button class="btn btn-link">Link</button>

<!-- Sizes -->
<button class="btn btn-xs">XS</button>
<button class="btn btn-sm">SM</button>
<button class="btn btn-md">MD</button>
<button class="btn btn-lg">LG</button>

<!-- Loading -->
<button class="btn loading">Loading</button>
```

### Card
```html
<div class="card w-96 bg-base-100 shadow-xl">
  <figure><img src="image.jpg" alt="" /></figure>
  <div class="card-body">
    <h2 class="card-title">Card Title</h2>
    <p>Card description here.</p>
    <div class="card-actions justify-end">
      <button class="btn btn-primary">Buy Now</button>
    </div>
  </div>
</div>
```

### Input
```html
<input type="text" placeholder="Type here" class="input input-bordered w-full max-w-xs" />
<input type="text" class="input input-primary" />
<input type="text" class="input input-error" />
```

### Form Control
```html
<div class="form-control w-full max-w-xs">
  <label class="label">
    <span class="label-text">Email</span>
  </label>
  <input type="email" class="input input-bordered" />
  <label class="label">
    <span class="label-text-alt">Error message</span>
  </label>
</div>
```

### Modal
```html
<button class="btn" onclick="my_modal.showModal()">Open Modal</button>
<dialog id="my_modal" class="modal">
  <div class="modal-box">
    <h3 class="font-bold text-lg">Hello!</h3>
    <p class="py-4">Modal content here.</p>
    <div class="modal-action">
      <form method="dialog">
        <button class="btn">Close</button>
      </form>
    </div>
  </div>
</dialog>
```

### Navbar
```html
<div class="navbar bg-base-100">
  <div class="flex-1">
    <a class="btn btn-ghost text-xl">Logo</a>
  </div>
  <div class="flex-none">
    <ul class="menu menu-horizontal px-1">
      <li><a>Link 1</a></li>
      <li><a>Link 2</a></li>
    </ul>
  </div>
</div>
```

### Alert
```html
<div class="alert alert-info">
  <span>Info message</span>
</div>
<div class="alert alert-success">
  <span>Success!</span>
</div>
<div class="alert alert-warning">
  <span>Warning!</span>
</div>
<div class="alert alert-error">
  <span>Error!</span>
</div>
```

### Badge
```html
<span class="badge">default</span>
<span class="badge badge-primary">primary</span>
<span class="badge badge-secondary">secondary</span>
```

### Table
```html
<div class="overflow-x-auto">
  <table class="table">
    <thead>
      <tr>
        <th>Name</th>
        <th>Email</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>John</td>
        <td>john@example.com</td>
      </tr>
    </tbody>
  </table>
</div>
```

---

## Custom Themes

```js
// tailwind.config.js
daisyui: {
  themes: [
    {
      mytheme: {
        "primary": "#3490dc",
        "secondary": "#ffed4a",
        "accent": "#38c172",
        "neutral": "#3d4451",
        "base-100": "#ffffff",
      },
    },
  ],
}
```
