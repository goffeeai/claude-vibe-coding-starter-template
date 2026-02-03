# Quick Start Guide

## 3 ขั้นตอนเริ่มต้น

### 1. ติดตั้ง Template
```bash
# Clone หรือ copy template เข้าโปรเจค
git clone https://github.com/goffeeai/claude-vibe-coding-starter-template.git .claude-template
cp -r .claude-template/.claude .claude-template/CLAUDE.md ./
rm -rf .claude-template
```

### 2. เลือก Rules ที่ใช้
เก็บเฉพาะไฟล์ที่ตรงกับ tech stack ของคุณ:
```
.claude/rules/
├── 00-prd.md           # ✅ เก็บไว้ - PRD โปรเจค
├── 01-overview.md      # ✅ เก็บไว้ - ภาพรวม
├── 02-ai-behavior.md   # ✅ เก็บไว้ - กฎพฤติกรรม AI
├── 09-changelog.md     # ✅ เก็บไว้ - บันทึกการเปลี่ยนแปลง
├── 99-credentials.local.md  # ✅ สร้างใหม่จาก example
├── ssr-nextjs.md       # ✅ เก็บไว้ถ้าใช้ Next.js
├── ui-tailwind.md      # ✅ เก็บไว้ถ้าใช้ Tailwind
└── db-postgresql.md    # ✅ เก็บไว้ถ้าใช้ PostgreSQL
```

### 3. สั่ง /start
เปิด Claude Code แล้วพิมพ์:
```
/start
```

---

## Tech Stack ที่รองรับ

### Frontend
- React, Vue, Svelte, Angular
- HTML/CSS/JS, Alpine.js, HTMX

### SSR Frameworks
- Next.js, Nuxt.js, SvelteKit
- Astro, Remix, AdonisJS

### Backend
- Express, Fastify, NestJS, Hono
- FastAPI, Django, Flask

### Database
- PostgreSQL, MySQL, SQLite, MongoDB
- Redis, Supabase, Firebase
- PlanetScale, Neon, Turso

### UI Frameworks
- Tailwind, DaisyUI, Shadcn/ui
- Bootstrap, NuxtUI, Flowbite

### Deployment
- VPS + SSH + PM2
- Docker + Docker Compose
- Cloudflare Tunnel + Nginx
- GitHub Actions CI/CD

---

## Skills ที่มี

| Skill | คำอธิบาย |
|-------|---------|
| `/start` | 🚀 เริ่มต้นโปรเจค / ทำความเข้าใจ codebase |
| `/save` | 💾 บันทึก context (local เท่านั้น) |
| `/save-github` | 📤 บันทึก + push GitHub |
| `/github` | 🔗 Push ขึ้น GitHub |
| `/help-me` | 🆘 ขอความช่วยเหลือแบบเป็นมิตร |
| `/show-creds` | 🔑 แสดง credentials ของโปรเจค |

---

## GitHub Push: Private vs Public

เมื่อใช้ `/github` หรือ `/save-github` และยังไม่มี repo:

| กรณี | แนะนำ |
|------|-------|
| มี API keys, passwords, secrets | 🔒 **Private** |
| โปรเจคส่วนตัว/บริษัท | 🔒 **Private** |
| Open source | 🌍 **Public** |
| Template/Portfolio | 🌍 **Public** |
| ไม่แน่ใจ | 🔒 **Private** |

---

## Tips

1. **แก้ไข PRD ก่อน** - ใส่รายละเอียดโปรเจคใน `00-prd.md`
2. **สร้าง credentials** - copy `99-credentials.example.md` เป็น `99-credentials.local.md`
3. **ลบไฟล์ที่ไม่ใช้** - ลด context ที่ AI ต้องโหลด
4. **อัพเดท changelog** - บันทึกทุกครั้งที่มีการเปลี่ยนแปลงสำคัญ
5. **ใช้ /save บ่อยๆ** - บันทึกงานก่อน context เต็ม
