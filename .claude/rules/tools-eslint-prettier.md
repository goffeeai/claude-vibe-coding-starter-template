# ESLint & Prettier

## Overview
- **ESLint**: Code linting (find problems)
- **Prettier**: Code formatting (consistent style)

---

## ESLint Setup

### Installation
```bash
npm install -D eslint @eslint/js typescript-eslint
```

### eslint.config.js (Flat Config)
```javascript
import js from '@eslint/js';
import tseslint from 'typescript-eslint';

export default [
  js.configs.recommended,
  ...tseslint.configs.recommended,
  {
    rules: {
      '@typescript-eslint/no-unused-vars': 'warn',
      'no-console': 'warn',
    },
  },
  {
    ignores: ['dist/', 'node_modules/'],
  },
];
```

---

## Prettier Setup

### Installation
```bash
npm install -D prettier
```

### .prettierrc
```json
{
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5",
  "printWidth": 100
}
```

### .prettierignore
```
dist
node_modules
*.md
```

---

## ESLint + Prettier Together

### Installation
```bash
npm install -D eslint-config-prettier eslint-plugin-prettier
```

### eslint.config.js
```javascript
import js from '@eslint/js';
import tseslint from 'typescript-eslint';
import prettier from 'eslint-plugin-prettier/recommended';

export default [
  js.configs.recommended,
  ...tseslint.configs.recommended,
  prettier,  // Must be last
];
```

---

## Scripts

```json
{
  "scripts": {
    "lint": "eslint src/",
    "lint:fix": "eslint src/ --fix",
    "format": "prettier --write src/",
    "format:check": "prettier --check src/"
  }
}
```

---

## VS Code Integration

### .vscode/settings.json
```json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "explicit"
  }
}
```

### Recommended Extensions
- ESLint (`dbaeumer.vscode-eslint`)
- Prettier (`esbenp.prettier-vscode`)

---

## Pre-commit Hook (Optional)

### Using lint-staged
```bash
npm install -D husky lint-staged
npx husky init
```

### package.json
```json
{
  "lint-staged": {
    "*.{js,ts,jsx,tsx}": ["eslint --fix", "prettier --write"],
    "*.{json,md}": ["prettier --write"]
  }
}
```

### .husky/pre-commit
```bash
npx lint-staged
```
