# Rules System Explained

## Rules คืออะไร?

Rules คือไฟล์ `.md` ที่อยู่ใน `.claude/rules/` ซึ่ง Claude Code จะโหลดอัตโนมัติทุกครั้งที่เปิดโปรเจค ทำให้ AI มี context เกี่ยวกับโปรเจคของคุณ

---

## หลักการตั้งชื่อ

```
.claude/rules/
├── 00-prd.md           # 00-09: Core project files
├── 01-overview.md
├── 09-changelog.md
├── runtime-*.md        # Runtime/platform
├── tools-*.md          # Dev tools
├── backend-*.md        # Backend frameworks
├── db-*.md             # Databases
├── orm-*.md            # ORMs
├── frontend-*.md       # Frontend frameworks
├── ssr-*.md            # SSR frameworks
├── ui-*.md             # UI frameworks
├── server-*.md         # Server/deployment
├── landing-*.md        # Landing page/SEO
└── 99-*.md             # 99: Local/secrets
```

---

## Core Files (00-09)

### 00-prd.md
Product Requirements Document:
- ชื่อโปรเจค
- วัตถุประสงค์
- Features หลัก
- User flows
- Technical requirements

### 01-overview.md
ภาพรวม tech stack:
- Frameworks ที่ใช้
- โครงสร้างโฟลเดอร์
- Commands ที่ใช้บ่อย

### 09-changelog.md
บันทึกการเปลี่ยนแปลง:
- Features ที่เพิ่ม
- Bugs ที่แก้
- Breaking changes

---

## Tech Stack Files

### runtime-*.md
- `runtime-nodejs.md` - Node.js
- `runtime-bun.md` - Bun
- `runtime-deno.md` - Deno

### backend-*.md
- `backend-express.md` - Express.js
- `backend-fastify.md` - Fastify
- `backend-hono.md` - Hono

### db-*.md
- `db-postgresql.md` - PostgreSQL
- `db-mysql.md` - MySQL
- `db-supabase.md` - Supabase

### orm-*.md
- `orm-prisma.md` - Prisma
- `orm-drizzle.md` - Drizzle
- `orm-lucid.md` - Lucid (AdonisJS)

### ssr-*.md
- `ssr-nextjs.md` - Next.js
- `ssr-nuxtjs.md` - Nuxt.js
- `ssr-adonisjs.md` - AdonisJS

### ui-*.md
- `ui-tailwind.md` - Tailwind CSS
- `ui-shadcn.md` - Shadcn/ui
- `ui-daisyui.md` - DaisyUI

---

## Local Files (99-*)

### 99-credentials.local.md
**สำคัญ: ไฟล์นี้ถูก gitignore**

เก็บ credentials ของโปรเจค:
- Database URLs
- API keys
- Server IPs
- Login credentials

---

## วิธีเลือก Rules

1. **ดู tech stack** - ใช้อะไรบ้าง?
2. **เก็บเฉพาะที่ใช้** - ลบที่ไม่เกี่ยว
3. **แก้ไขให้ตรง** - customize ตามโปรเจค

### ตัวอย่าง: Next.js + Tailwind + PostgreSQL

เก็บไว้:
```
00-prd.md
01-overview.md
09-changelog.md
ssr-nextjs.md
ui-tailwind.md
db-postgresql.md
orm-prisma.md
99-credentials.local.md
```

ลบทิ้ง:
```
runtime-*.md (Next.js จัดการเอง)
backend-*.md (Next.js API Routes)
ssr-nuxtjs.md, ssr-adonisjs.md
ui-bootstrap.md, ui-daisyui.md
db-mysql.md, db-mongodb.md
orm-drizzle.md, orm-lucid.md
```
