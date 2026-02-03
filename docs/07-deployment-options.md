# Deployment Options

## เลือก Deployment อย่างไร?

### Quick Decision

| ต้องการ | เลือก |
|---------|------|
| ง่ายสุด, frontend | **Vercel** / **Netlify** |
| Full-stack + DB | **Railway** / **Render** |
| ควบคุมเต็มที่ | **VPS** (DigitalOcean, Vultr) |
| เน้นราคา | **Hetzner** / **Contabo** |
| Enterprise | **AWS** / **GCP** / **Azure** |

---

## Platform Comparison

### Vercel
**ดีสำหรับ:** Next.js, Frontend
**ราคา:** Free tier + Usage-based
**ข้อดี:**
- Next.js integration เทพ
- Edge functions
- Preview deployments

```bash
# Deploy
npm i -g vercel
vercel
```

---

### Netlify
**ดีสำหรับ:** Static sites, Jamstack
**ราคา:** Free tier generous
**ข้อดี:**
- Form handling
- Split testing
- Identity (auth)

---

### Railway
**ดีสำหรับ:** Full-stack apps
**ราคา:** $5/month + usage
**ข้อดี:**
- Database included
- Easy environment variables
- GitHub integration

---

### Render
**ดีสำหรับ:** Full-stack, background workers
**ราคา:** Free tier + paid plans
**ข้อดี:**
- Auto-deploy from Git
- Managed PostgreSQL
- Cron jobs

---

### VPS (DIY)
**ดีสำหรับ:** Full control, cost-effective
**Providers:**
- DigitalOcean: $4-6/mo
- Vultr: $5/mo
- Hetzner: €4/mo
- Contabo: €5/mo

**Stack:**
```
Ubuntu 22.04
├── Nginx (reverse proxy)
├── Node.js + PM2
├── PostgreSQL / SQLite
└── Cloudflare Tunnel (SSL)
```

---

## VPS Deployment Guide

### 1. Server Setup
```bash
# SSH เข้า server
ssh root@your-server-ip

# Update system
apt update && apt upgrade -y

# Install Node.js
curl -fsSL https://deb.nodesource.com/setup_20.x | bash -
apt install -y nodejs

# Install PM2
npm install -g pm2

# Install Nginx
apt install -y nginx
```

### 2. Deploy App
```bash
# Clone project
cd /opt
git clone https://github.com/you/your-app.git
cd your-app

# Install & build
npm install
npm run build

# Start with PM2
pm2 start npm --name "my-app" -- start
pm2 save
pm2 startup
```

### 3. Nginx Config
```nginx
# /etc/nginx/sites-available/my-app
server {
    listen 80;
    server_name yourdomain.com;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

### 4. SSL with Certbot
```bash
apt install certbot python3-certbot-nginx
certbot --nginx -d yourdomain.com
```

---

## Cloudflare Tunnel (Alternative)

ไม่ต้องเปิด port, ไม่ต้อง SSL:

```bash
# Install cloudflared
curl -fsSL https://pkg.cloudflare.com/cloudflare-main.gpg | gpg --dearmor -o /usr/share/keyrings/cloudflare.gpg
echo "deb [signed-by=/usr/share/keyrings/cloudflare.gpg] https://pkg.cloudflare.com/cloudflared any main" | tee /etc/apt/sources.list.d/cloudflared.list
apt update && apt install cloudflared

# Login & create tunnel
cloudflared tunnel login
cloudflared tunnel create my-tunnel

# Config
cat > /etc/cloudflared/config.yml << EOF
tunnel: YOUR_TUNNEL_ID
credentials-file: /root/.cloudflared/YOUR_TUNNEL_ID.json

ingress:
  - hostname: yourdomain.com
    service: http://localhost:3000
  - service: http_status:404
EOF

# Run as service
cloudflared service install
systemctl start cloudflared
systemctl enable cloudflared
```

---

## Cost Comparison (Monthly)

```
┌─────────────────┬──────────┬──────────────────────────┐
│ Option          │ Cost     │ Best For                 │
├─────────────────┼──────────┼──────────────────────────┤
│ Vercel Free     │ $0       │ Hobby projects           │
│ Netlify Free    │ $0       │ Static sites             │
│ Railway         │ $5+      │ Full-stack startups      │
│ Render Free     │ $0       │ Learning, prototypes     │
│ Hetzner VPS     │ €4       │ Budget production        │
│ DigitalOcean    │ $6       │ Standard production      │
│ Vercel Pro      │ $20      │ Team/Commercial          │
│ AWS/GCP         │ $20+     │ Enterprise, scale        │
└─────────────────┴──────────┴──────────────────────────┘
```

---

## Recommendations

### Learning / Side Project
1. **Vercel** (Next.js) or **Netlify** (static)
2. Free, easy, good DX

### Startup / MVP
1. **Railway** - ง่าย, DB รวม
2. **VPS + Cloudflare Tunnel** - ประหยัด

### Production
1. **VPS** (Hetzner/DO) - คุ้มค่า
2. **Managed** (Vercel/Railway) - ถ้ามี budget
