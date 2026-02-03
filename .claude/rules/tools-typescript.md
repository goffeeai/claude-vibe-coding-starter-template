# TypeScript

## Overview
Typed superset of JavaScript

## Installation

```bash
npm install -D typescript
npx tsc --init  # Create tsconfig.json
```

---

## tsconfig.json

### Recommended for Node.js
```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "NodeNext",
    "moduleResolution": "NodeNext",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "outDir": "./dist",
    "rootDir": "./src"
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"]
}
```

### Recommended for Frontend (Vite)
```json
{
  "compilerOptions": {
    "target": "ES2020",
    "useDefineForClassFields": true,
    "lib": ["ES2020", "DOM", "DOM.Iterable"],
    "module": "ESNext",
    "skipLibCheck": true,
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx",
    "strict": true
  },
  "include": ["src"]
}
```

---

## Basic Types

```typescript
// Primitives
const name: string = "John";
const age: number = 25;
const active: boolean = true;

// Arrays
const numbers: number[] = [1, 2, 3];
const names: Array<string> = ["a", "b"];

// Objects
interface User {
  id: number;
  name: string;
  email?: string;  // Optional
}

// Functions
function greet(name: string): string {
  return `Hello, ${name}!`;
}

// Arrow functions
const add = (a: number, b: number): number => a + b;
```

---

## Common Patterns

### Type Aliases
```typescript
type ID = string | number;
type Status = "pending" | "active" | "done";
```

### Generics
```typescript
function first<T>(arr: T[]): T | undefined {
  return arr[0];
}

interface ApiResponse<T> {
  data: T;
  error?: string;
}
```

### Type Guards
```typescript
function isString(value: unknown): value is string {
  return typeof value === "string";
}
```

---

## Utility Types

```typescript
// Partial - all properties optional
type PartialUser = Partial<User>;

// Required - all properties required
type RequiredUser = Required<User>;

// Pick - select properties
type UserName = Pick<User, "name">;

// Omit - exclude properties
type UserWithoutId = Omit<User, "id">;

// Record - key-value mapping
type UserMap = Record<string, User>;
```

---

## Scripts

```json
{
  "scripts": {
    "build": "tsc",
    "dev": "tsc --watch",
    "typecheck": "tsc --noEmit"
  }
}
```

---

## Tips

1. Use `strict: true` always
2. Avoid `any`, use `unknown` instead
3. Use interfaces for objects, types for unions
4. Enable `skipLibCheck` for faster builds
