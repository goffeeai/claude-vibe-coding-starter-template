# Cloudflare

## Overview
DNS, CDN, and Tunnel for secure web access

---

## DNS Setup

1. Add domain to Cloudflare
2. Update nameservers at registrar
3. Add DNS records

### DNS Records
```
Type    Name        Content           Proxy
A       @           YOUR_SERVER_IP    Proxied
CNAME   www         @                 Proxied
CNAME   api         @                 Proxied
```

---

## Cloudflare Tunnel

### Install cloudflared
```bash
# Debian/Ubuntu
curl -fsSL https://pkg.cloudflare.com/cloudflare-main.gpg | sudo gpg --dearmor -o /usr/share/keyrings/cloudflare.gpg
echo "deb [signed-by=/usr/share/keyrings/cloudflare.gpg] https://pkg.cloudflare.com/cloudflared any main" | sudo tee /etc/apt/sources.list.d/cloudflared.list
sudo apt update && sudo apt install cloudflared
```

### Login & Create Tunnel
```bash
cloudflared tunnel login
cloudflared tunnel create my-tunnel
```

### Configure Tunnel
```bash
sudo mkdir -p /etc/cloudflared
sudo nano /etc/cloudflared/config.yml
```

```yaml
tunnel: YOUR_TUNNEL_ID
credentials-file: /root/.cloudflared/YOUR_TUNNEL_ID.json

ingress:
  - hostname: example.com
    service: http://localhost:3000
  - hostname: www.example.com
    service: http://localhost:3000
  - hostname: api.example.com
    service: http://localhost:8000
  - service: http_status:404
```

### Route DNS
```bash
cloudflared tunnel route dns my-tunnel example.com
cloudflared tunnel route dns my-tunnel www.example.com
```

### Run as Service
```bash
sudo cloudflared service install
sudo systemctl start cloudflared
sudo systemctl enable cloudflared
sudo systemctl status cloudflared
```

---

## Benefits

- **No open ports** - Server doesn't need port 80/443 open
- **Free SSL** - HTTPS automatically
- **DDoS protection** - Built-in
- **Zero Trust** - Optional access control

---

## Multiple Services

```yaml
# /etc/cloudflared/config.yml
tunnel: YOUR_TUNNEL_ID
credentials-file: /root/.cloudflared/YOUR_TUNNEL_ID.json

ingress:
  # Main app
  - hostname: example.com
    service: http://localhost:3000

  # API
  - hostname: api.example.com
    service: http://localhost:8000

  # Admin panel
  - hostname: admin.example.com
    service: http://localhost:3001

  # Catch-all
  - service: http_status:404
```

---

## Troubleshooting

```bash
# Check status
sudo systemctl status cloudflared

# View logs
sudo journalctl -u cloudflared -f

# Test tunnel
cloudflared tunnel run my-tunnel

# List tunnels
cloudflared tunnel list
```
