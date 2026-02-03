# Deno Runtime

## Overview
Secure runtime for JavaScript and TypeScript

## Installation

```bash
# macOS / Linux
curl -fsSL https://deno.land/install.sh | sh

# Windows (PowerShell)
irm https://deno.land/install.ps1 | iex

# Check version
deno --version
```

---

## Running Code

```bash
deno run src/main.ts           # Run file
deno run --watch src/main.ts   # Watch mode
deno run --allow-net src/main.ts  # With permissions
```

---

## Permissions

Deno is secure by default. Grant permissions explicitly:

```bash
--allow-read      # File system read
--allow-write     # File system write
--allow-net       # Network access
--allow-env       # Environment variables
--allow-run       # Run subprocesses
-A                # Allow all (development only)
```

Example:
```bash
deno run --allow-net --allow-env src/server.ts
```

---

## Importing Modules

### From URL
```typescript
import { serve } from "https://deno.land/std@0.200.0/http/server.ts";
```

### From npm
```typescript
import express from "npm:express@4";
```

### Import Map (deno.json)
```json
{
  "imports": {
    "std/": "https://deno.land/std@0.200.0/",
    "oak": "https://deno.land/x/oak@v12.6.1/mod.ts"
  }
}
```

---

## deno.json Configuration

```json
{
  "tasks": {
    "dev": "deno run --watch --allow-all src/main.ts",
    "start": "deno run --allow-all src/main.ts",
    "test": "deno test"
  },
  "imports": {
    "std/": "https://deno.land/std@0.200.0/"
  },
  "compilerOptions": {
    "strict": true
  }
}
```

---

## HTTP Server

### Using std library
```typescript
import { serve } from "https://deno.land/std@0.200.0/http/server.ts";

serve((req) => {
  return new Response("Hello from Deno!");
}, { port: 3000 });
```

### Using Oak (Express-like)
```typescript
import { Application, Router } from "https://deno.land/x/oak@v12.6.1/mod.ts";

const app = new Application();
const router = new Router();

router.get("/", (ctx) => {
  ctx.response.body = "Hello!";
});

app.use(router.routes());
await app.listen({ port: 3000 });
```

---

## Testing

```typescript
// src/math_test.ts
import { assertEquals } from "https://deno.land/std@0.200.0/assert/mod.ts";

Deno.test("addition", () => {
  assertEquals(2 + 2, 4);
});
```

```bash
deno test
```

---

## When to Use Deno

### ✅ Good for
- Security-focused applications
- TypeScript-first projects
- Single-file scripts
- Edge functions

### ⚠️ Consider alternatives for
- npm ecosystem heavy projects
- Existing Node.js codebases
