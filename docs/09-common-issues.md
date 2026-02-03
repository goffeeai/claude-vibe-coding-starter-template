# Common Issues & Solutions

## Development Issues

### Port already in use
```bash
# Find process using port
lsof -i :3000
# or on Windows
netstat -ano | findstr :3000

# Kill process
kill -9 <PID>
# or on Windows
taskkill /PID <PID> /F
```

### Node modules issues
```bash
# Clear cache and reinstall
rm -rf node_modules package-lock.json
npm cache clean --force
npm install
```

### Permission denied
```bash
# Fix npm permissions
sudo chown -R $(whoami) ~/.npm
sudo chown -R $(whoami) /usr/local/lib/node_modules
```

---

## Database Issues

### Connection refused
```bash
# Check if database is running
sudo systemctl status postgresql
sudo systemctl start postgresql

# Check connection string
# Wrong: postgres://localhost/db
# Right: postgres://user:pass@localhost:5432/db
```

### Migration failed
```bash
# Prisma
npx prisma migrate reset
npx prisma migrate dev

# Drizzle
npx drizzle-kit push:pg
```

### SQLite locked
```javascript
// ใช้ WAL mode
const db = new Database('app.db');
db.pragma('journal_mode = WAL');
```

---

## Build Issues

### Out of memory
```bash
# Increase Node memory
export NODE_OPTIONS="--max-old-space-size=4096"
npm run build

# หรือใน package.json
"scripts": {
  "build": "NODE_OPTIONS='--max-old-space-size=4096' next build"
}
```

### TypeScript errors
```bash
# Check types
npx tsc --noEmit

# Skip type check (temporary)
# next.config.js
module.exports = {
  typescript: {
    ignoreBuildErrors: true,
  },
};
```

### ESLint errors blocking build
```javascript
// next.config.js
module.exports = {
  eslint: {
    ignoreDuringBuilds: true,
  },
};
```

---

## Deployment Issues

### Build works locally but fails on server
```bash
# Check Node version matches
node -v

# Check environment variables are set
echo $DATABASE_URL

# Check dependencies
npm ci  # ใช้ ci แทน install
```

### PM2 not starting
```bash
# Check logs
pm2 logs app-name

# Restart with new config
pm2 delete app-name
pm2 start ecosystem.config.js

# Check memory
free -h
```

### Nginx 502 Bad Gateway
```bash
# Check app is running
curl localhost:3000

# Check nginx config
sudo nginx -t

# Check nginx logs
sudo tail -f /var/log/nginx/error.log
```

---

## Git Issues

### Accidentally committed secrets
```bash
# Remove from history
git filter-branch --force --index-filter \
  'git rm --cached --ignore-unmatch .env' \
  --prune-empty --tag-name-filter cat -- --all

# Force push
git push origin --force --all
```

### Merge conflicts
```bash
# See conflicts
git status

# Accept theirs
git checkout --theirs file.txt

# Accept ours
git checkout --ours file.txt

# After resolving
git add .
git commit
```

### Undo last commit
```bash
# Keep changes
git reset --soft HEAD~1

# Discard changes
git reset --hard HEAD~1
```

---

## Environment Issues

### .env not loading
```javascript
// ตรวจสอบว่า dotenv load แล้ว
import 'dotenv/config';
// หรือ
require('dotenv').config();

// Next.js ใช้ .env.local
// Nuxt.js ใช้ .env
```

### Environment variables undefined
```bash
# Check if set
printenv | grep MY_VAR

# Export in shell
export MY_VAR="value"

# Add to ~/.bashrc or ~/.zshrc
echo 'export MY_VAR="value"' >> ~/.bashrc
source ~/.bashrc
```

---

## Authentication Issues

### CORS errors
```javascript
// Express
app.use(cors({
  origin: 'http://localhost:3000',
  credentials: true,
}));

// Next.js API
res.setHeader('Access-Control-Allow-Origin', '*');
res.setHeader('Access-Control-Allow-Methods', 'GET, POST, PUT, DELETE');
```

### Cookies not working
```javascript
// Set secure flags correctly
res.cookie('token', value, {
  httpOnly: true,
  secure: process.env.NODE_ENV === 'production',
  sameSite: 'lax',
  maxAge: 7 * 24 * 60 * 60 * 1000, // 7 days
});
```

### Session lost after deploy
```javascript
// ใช้ persistent session store
// แทน in-memory (default)
import session from 'express-session';
import SQLiteStore from 'connect-sqlite3';

app.use(session({
  store: new SQLiteStore({ db: 'sessions.db' }),
  secret: process.env.SESSION_SECRET,
  resave: false,
  saveUninitialized: false,
}));
```

---

## Performance Issues

### Slow queries
```sql
-- Add indexes
CREATE INDEX idx_users_email ON users(email);

-- Check query plan
EXPLAIN ANALYZE SELECT * FROM users WHERE email = 'test@test.com';
```

### Memory leak
```bash
# Monitor memory
pm2 monit

# Set max memory restart
pm2 start app.js --max-memory-restart 500M
```

### Large bundle size
```bash
# Analyze bundle
npm run build -- --analyze

# Common fixes:
# - Dynamic imports
# - Tree shaking
# - Remove unused dependencies
```
