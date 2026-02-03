# SSH Setup

## Overview
Secure SSH configuration and key management

---

## Generate SSH Key

```bash
# Generate new key
ssh-keygen -t ed25519 -C "your@email.com"

# Or RSA (older systems)
ssh-keygen -t rsa -b 4096 -C "your@email.com"
```

Keys are saved to:
- Private: `~/.ssh/id_ed25519`
- Public: `~/.ssh/id_ed25519.pub`

---

## Copy Key to Server

```bash
# Easy way
ssh-copy-id -i ~/.ssh/id_ed25519.pub user@server

# Manual way
cat ~/.ssh/id_ed25519.pub | ssh user@server "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```

---

## SSH Config

```bash
# ~/.ssh/config

Host myserver
    HostName 103.91.205.252
    User root
    IdentityFile ~/.ssh/id_ed25519

Host production
    HostName prod.example.com
    User deploy
    IdentityFile ~/.ssh/id_prod
    Port 22

Host staging
    HostName staging.example.com
    User deploy
    IdentityFile ~/.ssh/id_staging
```

**Usage:**
```bash
ssh myserver
ssh production
```

---

## Server SSH Config

```bash
# /etc/ssh/sshd_config

Port 22
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
```

```bash
sudo systemctl restart sshd
```

---

## Common Commands

```bash
# Connect
ssh user@server
ssh -p 2222 user@server  # Custom port

# Copy files
scp file.txt user@server:/path/to/destination
scp -r folder user@server:/path/  # Directory

# Port forwarding
ssh -L 3000:localhost:3000 user@server

# Keep alive
ssh -o ServerAliveInterval=60 user@server
```

---

## Troubleshooting

```bash
# Debug connection
ssh -v user@server

# Check permissions
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub
chmod 600 ~/.ssh/authorized_keys

# Agent
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```
