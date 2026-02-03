# Vite

## Overview
Fast build tool and dev server for modern web projects

## Create New Project

```bash
# npm
npm create vite@latest my-app

# pnpm
pnpm create vite my-app

# With template
npm create vite@latest my-app -- --template react-ts
npm create vite@latest my-app -- --template vue-ts
npm create vite@latest my-app -- --template svelte-ts
```

---

## Project Structure

```
my-app/
├── public/           # Static assets (copied as-is)
├── src/
│   ├── assets/       # Processed assets
│   ├── components/
│   ├── App.tsx
│   └── main.tsx
├── index.html        # Entry HTML
├── vite.config.ts    # Vite config
├── tsconfig.json
└── package.json
```

---

## vite.config.ts

### Basic Config
```typescript
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';

export default defineConfig({
  plugins: [react()],
  server: {
    port: 3000,
  },
});
```

### With Path Aliases
```typescript
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import path from 'path';

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      '@': path.resolve(__dirname, './src'),
    },
  },
});
```

### With Proxy (API)
```typescript
export default defineConfig({
  server: {
    proxy: {
      '/api': {
        target: 'http://localhost:8000',
        changeOrigin: true,
      },
    },
  },
});
```

---

## Scripts

```json
{
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  }
}
```

---

## Environment Variables

### .env files
```
.env                # Loaded always
.env.local          # Loaded always, ignored by git
.env.development    # Loaded in dev
.env.production     # Loaded in production
```

### Usage
```env
VITE_API_URL=https://api.example.com
VITE_APP_TITLE=My App
```

```typescript
// Access in code (must start with VITE_)
const apiUrl = import.meta.env.VITE_API_URL;
```

---

## Static Assets

### In public/
```html
<!-- Accessed from root -->
<img src="/logo.png" />
```

### In src/assets/
```typescript
// Imported and processed
import logo from './assets/logo.png';
<img src={logo} />
```

---

## Build Output

```bash
npm run build
# Output in dist/
```

### Preview Production Build
```bash
npm run preview
```

---

## Common Plugins

```bash
# React
npm install -D @vitejs/plugin-react

# Vue
npm install -D @vitejs/plugin-vue

# Svelte
npm install -D @sveltejs/vite-plugin-svelte
```
