# VPS Setup

## Overview
Basic server setup for production deployment

---

## Initial Setup

### 1. Update System
```bash
apt update && apt upgrade -y
```

### 2. Create Non-root User
```bash
adduser deploy
usermod -aG sudo deploy
```

### 3. Setup SSH Key
```bash
# On your local machine
ssh-keygen -t ed25519 -C "your@email.com"

# Copy to server
ssh-copy-id -i ~/.ssh/id_ed25519.pub deploy@SERVER_IP

# Or manually
mkdir -p ~/.ssh
echo "YOUR_PUBLIC_KEY" >> ~/.ssh/authorized_keys
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

---

## Security

### Disable Password Auth
```bash
sudo nano /etc/ssh/sshd_config
```
```
PasswordAuthentication no
PubkeyAuthentication yes
PermitRootLogin no
```
```bash
sudo systemctl restart sshd
```

### Firewall (UFW)
```bash
sudo apt install ufw
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw allow 80
sudo ufw allow 443
sudo ufw enable
sudo ufw status
```

### Fail2ban
```bash
sudo apt install fail2ban
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

---

## Install Node.js

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs

# Verify
node -v
npm -v

# Install pnpm (optional)
npm install -g pnpm
```

---

## Install PM2

```bash
npm install -g pm2

# Run app
pm2 start npm --name "my-app" -- start

# Auto-start on boot
pm2 startup
pm2 save
```

---

## Deploy Code

```bash
# Create app directory
sudo mkdir -p /opt/my-app
sudo chown deploy:deploy /opt/my-app

# Clone repo
cd /opt
git clone https://github.com/user/repo.git my-app
cd my-app
npm install
npm run build

# Start with PM2
pm2 start npm --name "my-app" -- start
```

---

## Auto-deploy Script

```bash
#!/bin/bash
# deploy.sh

cd /opt/my-app
git pull
npm install
npm run build
pm2 restart my-app
```

---

## Useful Commands

```bash
# Check disk space
df -h

# Check memory
free -h

# Check processes
htop

# Check logs
pm2 logs
journalctl -u nginx

# Restart services
sudo systemctl restart nginx
pm2 restart all
```
