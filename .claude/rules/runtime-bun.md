# Bun Runtime

## Overview
Fast all-in-one JavaScript runtime & toolkit

## Installation

```bash
# macOS / Linux
curl -fsSL https://bun.sh/install | bash

# Windows (via scoop)
scoop install bun

# Check version
bun --version
```

---

## Package Management

```bash
bun install           # Install dependencies
bun add pkg           # Add package
bun add -D pkg        # Add dev dependency
bun remove pkg        # Remove package
bun update            # Update all
```

---

## Running Scripts

```bash
bun run dev           # Run script from package.json
bun run src/index.ts  # Run file directly
bun --watch src/index.ts  # Watch mode
```

---

## Key Features

### TypeScript Native
```typescript
// No config needed, just run
bun run src/index.ts
```

### Built-in Test Runner
```bash
bun test
```

```typescript
// src/math.test.ts
import { expect, test } from "bun:test";

test("2 + 2", () => {
  expect(2 + 2).toBe(4);
});
```

### Built-in Bundler
```bash
bun build ./src/index.ts --outdir ./dist
```

---

## Bun APIs

### File I/O
```typescript
// Read file
const file = Bun.file("./data.json");
const content = await file.text();

// Write file
await Bun.write("./output.txt", "Hello!");
```

### HTTP Server
```typescript
Bun.serve({
  port: 3000,
  fetch(req) {
    return new Response("Hello from Bun!");
  },
});
```

### SQLite (built-in)
```typescript
import { Database } from "bun:sqlite";

const db = new Database("mydb.sqlite");
db.run("CREATE TABLE IF NOT EXISTS users (id INTEGER PRIMARY KEY, name TEXT)");
```

---

## Compatibility

| Feature | Bun Support |
|---------|-------------|
| npm packages | ✅ Most work |
| Node.js APIs | ✅ Most supported |
| TypeScript | ✅ Native |
| JSX | ✅ Native |
| .env | ✅ Auto-loaded |

---

## When to Use Bun

### ✅ Good for
- New projects
- Fast development
- TypeScript projects
- Simple APIs

### ⚠️ Consider alternatives for
- Complex enterprise apps (Node.js more mature)
- Specific packages with compatibility issues
