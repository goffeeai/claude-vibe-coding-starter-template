# Project Structure

## โครงสร้างพื้นฐาน

```
my-project/
├── CLAUDE.md              # AI context index
├── .claude/
│   ├── rules/             # Auto-loaded documentation
│   │   ├── 00-prd.md
│   │   ├── 01-overview.md
│   │   ├── 09-changelog.md
│   │   └── 99-credentials.local.md
│   └── skills/            # Slash commands
│       ├── start/SKILL.md
│       ├── save-ct/SKILL.md
│       ├── help-me/SKILL.md
│       └── show-creds/SKILL.md
├── docs/                  # Project documentation
├── src/                   # Source code
├── .env                   # Environment variables
└── .gitignore
```

---

## ไฟล์สำคัญ

### CLAUDE.md
Index file ที่ AI อ่านอัตโนมัติเมื่อเปิดโปรเจค

### .claude/rules/
ไฟล์ทุกไฟล์ในนี้จะถูกโหลดอัตโนมัติ:
- `00-prd.md` - Product Requirements
- `01-overview.md` - Tech stack overview
- `09-changelog.md` - Change history
- `99-credentials.local.md` - Secrets (gitignored)

### .claude/skills/
Slash commands:
- `/start` - เริ่มต้นโปรเจค
- `/save-ct` - บันทึก context
- `/help-me` - ขอความช่วยเหลือ
- `/show-creds` - ดู credentials

---

## ตัวอย่าง Next.js Project

```
my-nextjs-app/
├── CLAUDE.md
├── .claude/
│   └── rules/
│       ├── 00-prd.md
│       ├── 01-overview.md
│       ├── ssr-nextjs.md
│       ├── ui-tailwind.md
│       ├── db-postgresql.md
│       ├── orm-prisma.md
│       └── 99-credentials.local.md
├── src/
│   ├── app/
│   ├── components/
│   └── lib/
├── prisma/
│   └── schema.prisma
├── .env.local
└── package.json
```

---

## ตัวอย่าง AdonisJS Project

```
my-adonis-app/
├── CLAUDE.md
├── .claude/
│   └── rules/
│       ├── 00-prd.md
│       ├── 01-overview.md
│       ├── ssr-adonisjs.md
│       ├── ui-tailwind.md
│       ├── db-postgresql.md
│       ├── orm-lucid.md
│       └── 99-credentials.local.md
├── app/
│   ├── controllers/
│   ├── models/
│   └── middleware/
├── resources/
│   └── views/
├── start/
│   └── routes.ts
├── .env
└── package.json
```
