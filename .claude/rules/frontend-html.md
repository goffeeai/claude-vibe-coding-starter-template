# HTML/CSS/JS

## Overview
Plain HTML, CSS, and JavaScript - no framework needed

## Project Structure

```
project/
├── index.html
├── css/
│   └── style.css
├── js/
│   └── main.js
├── images/
└── fonts/
```

---

## HTML Template

```html
<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Description here">
  <title>Page Title</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>
  <header>
    <nav>
      <a href="/">Home</a>
      <a href="/about">About</a>
    </nav>
  </header>

  <main>
    <h1>Hello World</h1>
  </main>

  <footer>
    <p>&copy; 2024</p>
  </footer>

  <script src="js/main.js"></script>
</body>
</html>
```

---

## CSS Best Practices

```css
/* Reset */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* Variables */
:root {
  --primary-color: #3490dc;
  --text-color: #333;
  --font-family: system-ui, sans-serif;
}

/* Base */
body {
  font-family: var(--font-family);
  color: var(--text-color);
  line-height: 1.6;
}

/* Responsive */
@media (max-width: 768px) {
  .container {
    padding: 1rem;
  }
}
```

---

## JavaScript (Modern)

```javascript
// DOM Ready
document.addEventListener('DOMContentLoaded', () => {
  // Code here
});

// Query elements
const button = document.querySelector('#submit');
const items = document.querySelectorAll('.item');

// Event listeners
button.addEventListener('click', handleClick);

// Fetch API
async function fetchData() {
  try {
    const response = await fetch('/api/data');
    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Error:', error);
  }
}

// DOM manipulation
const element = document.createElement('div');
element.textContent = 'Hello';
element.classList.add('active');
document.body.appendChild(element);
```

---

## With CDN Libraries

### Tailwind CSS
```html
<script src="https://cdn.tailwindcss.com"></script>
```

### Alpine.js
```html
<script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
```

### HTMX
```html
<script src="https://unpkg.com/htmx.org@1.9.x"></script>
```

---

## Development Server

```bash
# Using npx
npx serve

# Using Python
python -m http.server 8000

# Using PHP
php -S localhost:8000
```
