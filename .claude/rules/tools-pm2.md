# PM2 - Process Manager

## Overview
Production process manager for Node.js applications

## Installation

```bash
npm install -g pm2
```

---

## Basic Commands

```bash
# Start app
pm2 start app.js
pm2 start app.js --name "my-app"

# Start with npm script
pm2 start npm --name "my-app" -- start
pm2 start npm --name "my-app" -- run dev

# List processes
pm2 list
pm2 ls

# Stop
pm2 stop my-app
pm2 stop all

# Restart
pm2 restart my-app
pm2 restart all

# Delete
pm2 delete my-app
pm2 delete all

# Logs
pm2 logs
pm2 logs my-app
pm2 logs --lines 100
```

---

## Ecosystem File

### ecosystem.config.js
```javascript
module.exports = {
  apps: [{
    name: 'my-app',
    script: 'src/index.js',
    instances: 'max',        // Cluster mode
    exec_mode: 'cluster',
    env: {
      NODE_ENV: 'development',
      PORT: 3000
    },
    env_production: {
      NODE_ENV: 'production',
      PORT: 3000
    }
  }]
};
```

### Usage
```bash
pm2 start ecosystem.config.js
pm2 start ecosystem.config.js --env production
```

---

## Cluster Mode

```bash
# Run with all CPU cores
pm2 start app.js -i max

# Run with specific number
pm2 start app.js -i 4

# Scale up/down
pm2 scale my-app +2
pm2 scale my-app 4
```

---

## Monitoring

```bash
# Real-time monitoring
pm2 monit

# Show details
pm2 show my-app
pm2 info my-app

# Memory/CPU metrics
pm2 list
```

---

## Startup Script

```bash
# Generate startup script
pm2 startup

# Save current process list
pm2 save

# Restore saved processes
pm2 resurrect
```

ทำให้ PM2 รันอัตโนมัติเมื่อ server restart

---

## Log Management

```bash
# View logs
pm2 logs

# Clear logs
pm2 flush

# Log rotation (install module)
pm2 install pm2-logrotate

# Configure rotation
pm2 set pm2-logrotate:max_size 10M
pm2 set pm2-logrotate:retain 7
```

---

## Common Patterns

### Auto-restart on file change (Development)
```bash
pm2 start app.js --watch
pm2 start app.js --watch --ignore-watch="node_modules"
```

### Memory limit
```bash
pm2 start app.js --max-memory-restart 300M
```

### Delay between restarts
```bash
pm2 start app.js --restart-delay=3000
```

---

## Useful Aliases

```bash
# Add to ~/.bashrc or ~/.zshrc
alias pml='pm2 list'
alias pmlog='pm2 logs'
alias pmr='pm2 restart all'
alias pms='pm2 stop all'
```
