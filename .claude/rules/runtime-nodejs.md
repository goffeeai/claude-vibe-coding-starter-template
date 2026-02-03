# Node.js Runtime

## Overview
JavaScript runtime สำหรับ server-side development

## Version Management

### nvm (Node Version Manager)
```bash
# Install nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash

# Install Node.js
nvm install 20
nvm use 20
nvm alias default 20

# Check version
node -v
npm -v
```

### fnm (Fast Node Manager)
```bash
# Install fnm
curl -fsSL https://fnm.vercel.app/install | bash

# Install Node.js
fnm install 20
fnm use 20
fnm default 20
```

---

## Package Managers

### npm (default)
```bash
npm install           # Install dependencies
npm install pkg       # Add package
npm install -D pkg    # Add dev dependency
npm run dev           # Run script
npm run build         # Build
```

### pnpm (recommended)
```bash
# Install pnpm
npm install -g pnpm

pnpm install          # Install dependencies
pnpm add pkg          # Add package
pnpm add -D pkg       # Add dev dependency
pnpm dev              # Run script
```

### yarn
```bash
# Install yarn
npm install -g yarn

yarn                  # Install dependencies
yarn add pkg          # Add package
yarn add -D pkg       # Add dev dependency
yarn dev              # Run script
```

---

## package.json Structure

```json
{
  "name": "project-name",
  "version": "1.0.0",
  "type": "module",
  "scripts": {
    "dev": "node --watch src/index.js",
    "start": "node src/index.js",
    "build": "..."
  },
  "dependencies": {},
  "devDependencies": {}
}
```

### CommonJS vs ESM

| Feature | CommonJS | ESM |
|---------|----------|-----|
| Import | `require()` | `import` |
| Export | `module.exports` | `export` |
| File ext | `.js` or `.cjs` | `.js` or `.mjs` |
| package.json | default | `"type": "module"` |

---

## Environment Variables

### .env file
```env
NODE_ENV=development
PORT=3000
DATABASE_URL=postgresql://...
API_KEY=xxx
```

### Loading .env
```javascript
// With dotenv package
import 'dotenv/config';

// Access
const port = process.env.PORT || 3000;
```

### .env.example
```env
NODE_ENV=development
PORT=3000
DATABASE_URL=
API_KEY=
```

---

## Common Patterns

### Async/Await
```javascript
async function fetchData() {
  try {
    const response = await fetch(url);
    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Error:', error);
    throw error;
  }
}
```

### Error Handling
```javascript
// Global error handler
process.on('uncaughtException', (error) => {
  console.error('Uncaught Exception:', error);
  process.exit(1);
});

process.on('unhandledRejection', (reason, promise) => {
  console.error('Unhandled Rejection:', reason);
});
```

---

## Recommended Node.js Version
- **LTS (Long Term Support)**: Node.js 20.x or 22.x
- Check: https://nodejs.org/en/about/releases/
