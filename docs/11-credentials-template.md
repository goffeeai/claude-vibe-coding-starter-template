# Credentials Template

## วิธีใช้งาน

1. Copy ไฟล์นี้ไปที่ `.claude/rules/99-credentials.local.md`
2. แก้ไขข้อมูลตามโปรเจคจริง
3. ไฟล์นี้ถูก gitignore อยู่แล้ว (ปลอดภัย)

---

## Template

```markdown
# Project Credentials

> ⚠️ ไฟล์นี้ถูก gitignore - ไม่ถูก commit

## Project Info
- **Name**: [ชื่อโปรเจค]
- **Production URL**: https://...
- **Staging URL**: https://...
- **Local URL**: http://localhost:3000

---

## Database

### Production
- **Type**: PostgreSQL
- **Host**: db.example.com
- **Port**: 5432
- **Database**: myapp_prod
- **User**: myapp
- **Password**: [password]
- **Connection String**:
  ```
  postgres://myapp:password@db.example.com:5432/myapp_prod
  ```

### Development
- **Type**: SQLite
- **Path**: ./data/dev.db

---

## Server Access

### Production Server
- **IP**: 123.45.67.89
- **User**: deploy
- **SSH Key**: ~/.ssh/id_prod
- **SSH Command**: `ssh deploy@123.45.67.89`

### Staging Server
- **IP**: 123.45.67.90
- **User**: deploy
- **SSH Key**: ~/.ssh/id_staging

---

## API Keys

### Stripe
- **Publishable Key**: pk_live_...
- **Secret Key**: sk_live_...
- **Webhook Secret**: whsec_...

### Cloudflare
- **Account ID**: ...
- **API Token**: ...
- **Tunnel ID**: ...

### SendGrid / Email
- **API Key**: SG...

### Google
- **Client ID**: ...
- **Client Secret**: ...

---

## Admin Accounts

### Dashboard Admin
- **URL**: https://admin.example.com
- **Email**: admin@example.com
- **Password**: [password]

### Database Admin (pgAdmin/Adminer)
- **URL**: https://db-admin.example.com
- **User**: admin
- **Password**: [password]

---

## Third-party Services

### Vercel
- **Team**: my-team
- **Project**: my-project
- **Domain**: example.com

### Supabase
- **Project URL**: https://xxx.supabase.co
- **Anon Key**: eyJ...
- **Service Role Key**: eyJ...

### GitHub
- **Repo**: https://github.com/user/repo
- **Deploy Token**: ghp_...

---

## Environment Variables

### .env.local (Development)
```env
DATABASE_URL="postgres://..."
NEXTAUTH_SECRET="random-secret"
NEXTAUTH_URL="http://localhost:3000"
STRIPE_SECRET_KEY="sk_test_..."
```

### .env.production
```env
DATABASE_URL="postgres://..."
NEXTAUTH_SECRET="random-secret"
NEXTAUTH_URL="https://example.com"
STRIPE_SECRET_KEY="sk_live_..."
```

---

## Notes
- Last updated: [date]
- Updated by: [name]
```

---

## Security Tips

1. **อย่า commit** - ตรวจสอบ .gitignore
2. **ใช้ environment variables** - ไม่ hardcode ใน code
3. **Rotate regularly** - เปลี่ยน password/key เป็นระยะ
4. **Different per environment** - Dev/Staging/Prod แยกกัน
5. **Least privilege** - ให้สิทธิ์เท่าที่จำเป็น

---

## Quick Commands

### ดู credentials
```
/show-creds
```

### ตรวจสอบ .gitignore
```bash
git status
# ไฟล์ 99-credentials.local.md ต้องไม่โชว์
```

### ตรวจสอบว่าไม่ได้ commit
```bash
git log --all --full-history -- "**/99-credentials*"
# ควรว่างเปล่า
```
