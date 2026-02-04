# 🚀 Claude Vibe Coding Starter Template

![Claude](https://img.shields.io/badge/Claude-Ready-blue)
![Skills](https://img.shields.io/badge/Skills-8-orange)
![Stack](https://img.shields.io/badge/Tech_Stack-50+-purple)
![PRD](https://img.shields.io/badge/PRD-Included-green)
![Rules](https://img.shields.io/badge/Rules-64-red)

**Claude Skills • Tech Stack • PRD • Rules** - All-in-one Template

> ⚡ Skills | 🛠️ Tech Stack | 📋 PRD | 📚 Rules | 🤖 Claude

**Language / ภาษา:** [🇹🇭 TH ไทย](#-ก่อนเริ่มต้น) | [🇺🇸 EN English](#-english)

---

## 🎯 วิธีใช้งาน (3 ขั้นตอน)

### 1. เปิดโปรแกรมที่จะใช้ Vibe Code

> **หมายเหตุ:** Template นี้ออกแบบมาสำหรับ **Claude** เป็นหลัก
> AI ตัวอื่นก็ใช้ได้ แต่ต้องสั่งให้อ่านโฟลเดอร์ `.claude/` เอง

| IDE | รองรับ Claude |
|-----|---------------|
| **VS Code** | ✅ Extension / CLI |
| **Cursor** | ✅ Claude built-in / Extension / CLI |
| **Windsurf** | ✅ Claude built-in / Extension / CLI |
| **Antigravity** | ✅ Claude built-in / Extension / CLI |

### 2. ติดตั้ง Template

เริ่มทำโปรเจคใหม่ Copy ไปวางได้เลย
```
ช่วย clone https://github.com/goffeeai/claude-vibe-coding-starter-template
มาที่โฟลเดอร์นี้โดยตรง (ไม่ต้องสร้างโฟลเดอร์ย่อย)
```

กรณี มีโปรเจคอยู่แล้วอยากทำต่อ ให้ใช้อันนี้
```
ช่วย copy .claude/ และ docs/ จาก
https://github.com/goffeeai/claude-vibe-coding-starter-template
มาที่โปรเจคนี้ให้หน่อยครับ
```

### 3. เริ่มใช้งาน

พอติดตั้งเสร็จแล้ว พิมพ์:
```
/start
```
ถ้าพิมพ์ `/start` ไม่ขึ้น → กด `Ctrl+Shift+P` พิมพ์ `Reload Window` แล้วลองใหม่

**เสร็จแล้ว!** AI จะ guide ขั้นตอนถัดไปให้ครับ 🎉

---

## 🎮 คำสั่งลัด (Skills)

| พิมพ์ | ทำอะไร |
|-------|--------|
| `/start` | 🚀 **เริ่มใช้งาน** - ใช้ครั้งแรกที่เปิดโปรเจค |
| `/save` | 💾 **บันทึกงาน** - อัพเดท changelog, บันทึกปัญหา/วิธีแก้ → AI ทำงานต่อได้แม้ context reset |
| `/save-github` | 📤 **บันทึก + push** - ทำทุกอย่างเหมือน /save แล้ว push ขึ้น GitHub |
| `/github` | 🔗 Push ขึ้น GitHub (ถ้ายังไม่มี repo จะถาม Private/Public) |
| `/test` | 🧪 รัน tests + auto-fix (ถ้ามี test framework) |
| `/help-me` | 🆘 ติดปัญหา ต้องการความช่วยเหลือ |
| `/show-creds` | 🔑 ดู credentials ของโปรเจค |
| `/seo` | 🔍 **SEO Expert Mode** - สร้างหน้าเว็บที่ติด Google และ AI เข้าใจ |

---

## 📌 ใช้ Template นี้ตอนไหน?

### ✅ ใช้เลยตั้งแต่แรก (แนะนำ)

```
สร้างโปรเจคใหม่
      ↓
Copy template นี้ลงไป
      ↓
พิมพ์ /start
      ↓
AI ช่วย setup ให้
      ↓
เริ่ม coding!
```

### ✅ ใช้หลังคุยกับ AI ไปแล้ว

```
คุยกับ AI ไปสักพัก
      ↓
รู้แล้วว่าจะทำอะไร ใช้ stack อะไร
      ↓
Copy template นี้ลงไป
      ↓
พิมพ์ /start
      ↓
AI customize ให้ตาม stack
```

### ❌ ไม่ต้องใช้เมื่อ

- ถามคำถามสั้นๆ ไม่ได้ทำโปรเจค
- ทดลองโค้ดเล็กๆ น้อยๆ

---

## 📁 โครงสร้าง Template

```
claude-vibe-coding-starter-template/
│
├── 📄 README.md          ← คุณอยู่ที่นี่!
├── 📄 CLAUDE.md          ← AI อ่านไฟล์นี้ทุกครั้ง
│
├── 📁 .claude/
│   ├── 📁 rules/         ← เอกสารให้ AI อ่าน
│   │   ├── 00-prd.md           ← PRD (ความต้องการ)
│   │   ├── 01-overview.md      ← ภาพรวมโปรเจค
│   │   ├── 03-architecture.md  ← โครงสร้างโปรเจค ⭐
│   │   ├── 04-decisions.md     ← การตัดสินใจสำคัญ ⭐
│   │   ├── 09-changelog.md     ← บันทึกการเปลี่ยนแปลง
│   │   └── ...                 ← Tech stack rules
│   └── 📁 skills/        ← คำสั่งลัด (/start, /save, /test, ฯลฯ)
│
└── 📁 docs/              ← เอกสารสำหรับคนอ่าน + วิธี setup เครื่อง
```

---

## 🤔 FAQ

### ⚡ ก่อนเริ่มต้น

**🆕 มือใหม่มาก (ยังไม่เคย coding)**

ถ้ายังไม่มี Git หรือ Node.js ในเครื่อง:
→ อ่าน [วิธี Setup เครื่องใหม่](docs/12-setup-new-machine.md) ก่อน

รองรับ: **Windows**, **macOS**, **Linux**

**✅ พร้อมแล้ว (มี Git + Node.js แล้ว)**

→ ข้ามไปขั้นตอน "วิธีใช้งาน" ด้านล่างได้เลย

---

### Q: ต้อง copy ทุกไฟล์ใน rules/ ไหม?

**ไม่ต้อง!** พิมพ์ `/start` แล้ว AI จะเลือกไฟล์ที่เกี่ยวข้องให้

ตัวอย่าง:
- ทำเว็บด้วย **Next.js** → AI เลือก `ssr-nextjs.md`, `ui-tailwind.md`, ...
- ทำ **API** อย่างเดียว → AI เลือก `backend-express.md`, `db-postgresql.md`, ...

---

### Q: context ใกล้เต็ม คืออะไร?

AI มีหน่วยความจำจำกัด เมื่อคุยนานๆ จะเริ่มลืมเรื่องเก่า

**วิธีสังเกต:** IDE จะแสดง context usage

**วิธีแก้:** พิมพ์ `/save` หรือ `/save-github` เพื่อบันทึกงานก่อน context หาย

---

### Q: /save vs /save-github ต่างกันยังไง?

| Command | บันทึก Local | Push GitHub |
|---------|-------------|-------------|
| `/save` | ✅ | ❌ |
| `/save-github` | ✅ | ✅ |
| `/github` | ❌ | ✅ |

---

### Q: ย้ายไปทำเครื่องอื่นได้ไหม?

ได้! ทำตามนี้:

1. เครื่องเก่า: `/save-github` → push ขึ้น GitHub
2. เครื่องใหม่: `git clone` → เปิด IDE
3. พิมพ์ `/start` แล้วเลือก "กลับมาทำต่อ"

---

### Q: ทำงานเป็นทีมได้ไหม?

ได้! ทุกคนใช้ template เดียวกัน

- `.claude/rules/` → commit ขึ้น Git (ทีมเห็นเหมือนกัน)
- `99-credentials.local.md` → ไม่ commit (แต่ละคนใส่เอง)

---

### Q: Private หรือ Public repo ดี?

| กรณี | แนะนำ |
|------|-------|
| มี API keys, passwords | 🔒 **Private** |
| โปรเจคส่วนตัว/บริษัท | 🔒 **Private** |
| Open source | 🌍 **Public** |
| Template/Portfolio | 🌍 **Public** |
| ไม่แน่ใจ | 🔒 **Private** (ปลอดภัยกว่า) |

---

## 📖 เอกสารเพิ่มเติม

| ไฟล์ | เนื้อหา |
|------|--------|
| [docs/00-quick-start.md](docs/00-quick-start.md) | เริ่มต้น 5 นาที |
| [docs/03-skills-guide.md](docs/03-skills-guide.md) | วิธีใช้ Skills |
| [docs/06-database-selection.md](docs/06-database-selection.md) | วิธีเลือก database |
| [docs/07-deployment-options.md](docs/07-deployment-options.md) | ขึ้น production |
| [docs/10-git-workflow.md](docs/10-git-workflow.md) | Git พื้นฐาน |

---

## 💡 Tips สำหรับมือใหม่

1. **เริ่มจากโปรเจคเล็กๆ** - Landing page, Todo app
2. **ใช้ `/help-me` ได้เลย** - AI พร้อมช่วยเสมอ
3. **อย่าลืม `/save`** - บันทึกงานบ่อยๆ
4. **ถาม AI ได้ทุกเรื่อง** - ยินดีตอบทุกคำถาม

---

## 🛠️ Tech Stack ที่รองรับ

### Frontend
React, Vue, Svelte, Angular, HTML/CSS, Alpine.js, HTMX

### SSR Frameworks
Next.js, Nuxt.js, SvelteKit, Astro, Remix, AdonisJS

### Backend
Express, Fastify, NestJS, Hono, FastAPI, Django, Flask

### Database
PostgreSQL, MySQL, SQLite, MongoDB, Redis, Supabase, Firebase

### UI
Tailwind, Bootstrap, DaisyUI, Shadcn/ui, MUI, Vuetify, Chakra UI, NuxtUI

---

## 📝 Changelog

- **v1.3** - เพิ่ม `/test` skill พร้อม auto-fix, Zustand, React Hook Form + Zod rules
- **v1.2** - เพิ่ม SEO/AEO guide, Astro+Starlight rules, UI Framework recommendation
- **v1.1** - เพิ่ม `/save`, `/save-github`, `/github` skills
- **v1.0** - Initial release

---

# 🇬🇧 English

All-in-one **Skills**, **Tech Stack**, **PRD**, **Rules** template for **Claude** - Organize your project efficiently, perfect for beginners and pros

---

## ⚡ Before You Start

### 🆕 Complete Beginner (Never coded before)

If you don't have Git or Node.js installed:
→ Read [New Machine Setup Guide](docs/12-setup-new-machine.md) first

Supports: **Windows**, **macOS**, **Linux**

### ✅ Ready to Go (Git + Node.js installed)

→ Skip to "How to Use" section below

---

## 🎯 How to Use (3 Steps)

### 1. Open an IDE with AI Assistant

> **Note:** This template is designed primarily for **Claude**.
> Other AI assistants can use it, but need to be instructed to read the `.claude/` folder.

| IDE | Claude Support |
|-----|----------------|
| **VS Code** | ✅ Extension / CLI |
| **Cursor** | ✅ Claude built-in / Extension / CLI |
| **Windsurf** | ✅ Claude built-in / Extension / CLI |
| **Antigravity** | ✅ Claude built-in / Extension / CLI |

### 2. Install Template

Tell AI:
```
Please clone https://github.com/goffeeai/claude-vibe-coding-starter-template
directly into this folder (don't create a subfolder)
```

Or if you already have a project:
```
Please copy .claude/ and docs/ from
https://github.com/goffeeai/claude-vibe-coding-starter-template
to this project
```

### 3. Start Using

After installation, type:
```
/start
```
If `/start` doesn't work → Press `Ctrl+Shift+P`, type `Reload Window`, then try again

**Done!** AI will guide you through the next steps 🎉

---

## 🎮 Shortcuts (Skills)

| Command | Action |
|---------|--------|
| `/start` | 🚀 **Get Started** - Use when first opening project |
| `/save` | 💾 **Save work** - Update changelog, record issues/solutions → AI continues seamlessly after context reset |
| `/save-github` | 📤 **Save + push** - Everything /save does, then push to GitHub |
| `/github` | 🔗 Push to GitHub (asks Private/Public if no repo) |
| `/test` | 🧪 Run tests + auto-fix (if test framework exists) |
| `/help-me` | 🆘 Stuck, need help |
| `/show-creds` | 🔑 View project credentials |
| `/seo` | 🔍 **SEO Expert Mode** - Create SEO-friendly pages for Google and AI |

---

## 📌 When to Use This Template?

### ✅ Use from the Start (Recommended)

```
Create new project
      ↓
Copy this template
      ↓
Type /start
      ↓
AI helps setup
      ↓
Start coding!
```

### ✅ Use After Chatting with AI

```
Chat with AI for a while
      ↓
Know what to build and which stack
      ↓
Copy this template
      ↓
Type /start
      ↓
AI customizes for your stack
```

### ❌ Don't Need When

- Quick questions, not building a project
- Testing small code snippets

---

## 📁 Template Structure

```
claude-vibe-coding-starter-template/
│
├── 📄 README.md          ← You are here!
├── 📄 CLAUDE.md          ← AI reads this every time
│
├── 📁 .claude/
│   ├── 📁 rules/         ← AI documentation
│   │   ├── 00-prd.md           ← PRD (requirements)
│   │   ├── 01-overview.md      ← Project overview
│   │   ├── 03-architecture.md  ← Project structure ⭐
│   │   ├── 04-decisions.md     ← Key decisions ⭐
│   │   ├── 09-changelog.md     ← Change log
│   │   └── ...                 ← Tech stack rules
│   └── 📁 skills/        ← Shortcuts (/start, /save, /test, etc.)
│
└── 📁 docs/              ← Human-readable docs + machine setup guide
```

---

## 🤔 FAQ

### Q: Do I need to copy all files in rules/?

**No!** Type `/start` and AI will select relevant files for you

Examples:
- Building with **Next.js** → AI selects `ssr-nextjs.md`, `ui-tailwind.md`, ...
- Building **API** only → AI selects `backend-express.md`, `db-postgresql.md`, ...

---

### Q: What is "context almost full"?

AI has limited memory. After long conversations, it starts forgetting earlier content.

**How to notice:** IDE shows context usage

**Solution:** Type `/save` or `/save-github` to save work before context resets

---

### Q: What's the difference between /save and /save-github?

| Command | Save Local | Push GitHub |
|---------|------------|-------------|
| `/save` | ✅ | ❌ |
| `/save-github` | ✅ | ✅ |
| `/github` | ❌ | ✅ |

---

### Q: Can I continue on another machine?

Yes! Follow these steps:

1. Old machine: `/save-github` → push to GitHub
2. New machine: `git clone` → open IDE
3. Type `/start` and select "Continue working"

---

### Q: Can I work with a team?

Yes! Everyone uses the same template

- `.claude/rules/` → commit to Git (team sees same rules)
- `99-credentials.local.md` → not committed (each person adds their own)

---

### Q: Private or Public repo?

| Case | Recommendation |
|------|----------------|
| Has API keys, passwords | 🔒 **Private** |
| Personal/company project | 🔒 **Private** |
| Open source | 🌍 **Public** |
| Template/Portfolio | 🌍 **Public** |
| Not sure | 🔒 **Private** (safer) |

---

## 📖 Additional Documentation

| File | Content |
|------|---------|
| [docs/00-quick-start.md](docs/00-quick-start.md) | 5-minute quickstart |
| [docs/03-skills-guide.md](docs/03-skills-guide.md) | How to use Skills |
| [docs/06-database-selection.md](docs/06-database-selection.md) | Choosing a database |
| [docs/07-deployment-options.md](docs/07-deployment-options.md) | Production deployment |
| [docs/10-git-workflow.md](docs/10-git-workflow.md) | Git basics |

---

## 💡 Tips for Beginners

1. **Start with small projects** - Landing page, Todo app
2. **Use `/help-me` anytime** - AI is always ready to help
3. **Don't forget `/save`** - Save work frequently
4. **Ask AI anything** - No question is too basic

---

## 🛠️ Supported Tech Stack

### Frontend
React, Vue, Svelte, Angular, HTML/CSS, Alpine.js, HTMX

### SSR Frameworks
Next.js, Nuxt.js, SvelteKit, Astro, Remix, AdonisJS

### Backend
Express, Fastify, NestJS, Hono, FastAPI, Django, Flask

### Database
PostgreSQL, MySQL, SQLite, MongoDB, Redis, Supabase, Firebase

### UI
Tailwind, Bootstrap, DaisyUI, Shadcn/ui, MUI, Vuetify, Chakra UI, NuxtUI

---

## 📝 Changelog

- **v1.3** - Added `/test` skill with auto-fix, Zustand, React Hook Form + Zod rules
- **v1.2** - Added SEO/AEO guide, Astro+Starlight rules, UI Framework recommendation
- **v1.1** - Added `/save`, `/save-github`, `/github` skills
- **v1.0** - Initial release

---

Made with ❤️ for Vibe Coders
