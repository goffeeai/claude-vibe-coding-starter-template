# Credentials Template

> 💡 Copy ไฟล์นี้เป็น `99-credentials.local.md` แล้วใส่ข้อมูลจริง
> ไฟล์ `.local.md` จะไม่ถูก commit ขึ้น Git

---

## 🌐 URLs

| Environment | URL |
|-------------|-----|
| Production | https://example.com |
| Staging | https://staging.example.com |
| Development | http://localhost:3000 |

---

## 🖥️ Servers

| Server | IP | SSH User | หมายเหตุ |
|--------|-----|----------|----------|
| Production | 103.xxx.xxx.xxx | root | DigitalOcean |
| Database | - | - | อยู่เครื่องเดียวกัน |

---

## 🔐 Admin / Dashboard Login

| ระบบ | URL | Username | Password |
|------|-----|----------|----------|
| Admin Panel | /admin | admin | xxxxxx |
| Database GUI | /adminer | root | xxxxxx |

---

## 🗄️ Database

| Type | Host | Port | Database | User | Password |
|------|------|------|----------|------|----------|
| PostgreSQL | localhost | 5432 | myapp_db | myapp | xxxxxx |

---

## 🔑 API Keys & Services

| Service | Key Name | หมายเหตุ |
|---------|----------|----------|
| Cloudflare | API Token | สำหรับ DNS |
| Stripe | sk_live_xxx | Payment |
| SendGrid | SG.xxx | Email |

---

## 📧 Email / Accounts

| Service | Email | Password | หมายเหตุ |
|---------|-------|----------|----------|
| GitHub | dev@example.com | xxxxxx | repo owner |
| Cloudflare | dev@example.com | xxxxxx | DNS |

---

## 🔗 Important Links

| ชื่อ | Link |
|------|------|
| GitHub Repo | https://github.com/xxx/xxx |
| Cloudflare Dashboard | https://dash.cloudflare.com |
| Design (Figma) | https://figma.com/xxx |
| Docs (Notion) | https://notion.so/xxx |

---

## 📝 Notes

- SSH Key อยู่ที่: `~/.ssh/id_rsa_projectname`
- Backup database ทุกวัน 02:00 น.
- SSL auto-renew ผ่าน Cloudflare
