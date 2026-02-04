---
name: find-skills
description: ติดตั้งและใช้งาน find-skills จาก skills.sh
user-invocable: true
---

# Find Skills - ค้นหา Agent Skills

> Credit: [skills.sh](https://skills.sh) by Vercel Labs

## เมื่อ user พิมพ์ /find-skills

### ขั้นตอนที่ 1: ตรวจสอบว่าติดตั้ง find-skills หรือยัง

ตรวจสอบว่ามีโฟลเดอร์ `.agents/skills/find-skills/` หรือไฟล์ที่เกี่ยวข้องหรือไม่

**ถ้ายังไม่มี:**
```bash
npx skills add vercel-labs/skills/find-skills
```

เลือก options:
- Agent: เลือกตาม IDE ที่ user ใช้ (Claude Code, Cursor, Windsurf, etc.)
- Scope: Current directory (recommended)
- Method: Symlink (recommended)

**ถ้ามีแล้ว:** ข้ามไปขั้นตอนที่ 2

---

### ขั้นตอนที่ 2: ถาม user ว่าต้องการค้นหาอะไร

ถาม: "ต้องการค้นหา skill เกี่ยวกับอะไร?"

ตัวอย่าง:
- React performance
- Testing
- TypeScript
- Database
- UI/UX design

---

### ขั้นตอนที่ 3: ค้นหาด้วย find-skills

ใช้คำสั่ง:
```bash
npx skills find [keyword]
```

หรือถ้าติดตั้ง find-skills แล้ว AI จะค้นหาให้อัตโนมัติ

---

### ขั้นตอนที่ 4: ช่วยติดตั้ง skill ที่เลือก

เมื่อ user เลือก skill แล้ว:
```bash
npx skills add <owner/repo>
```

---

## Quick Reference

```bash
# ค้นหา skill
npx skills find [keyword]

# ติดตั้ง skill
npx skills add <owner/repo>

# ดู skills ที่ติดตั้งแล้ว
npx skills list

# อัพเดท skills
npx skills update
```

---

## Skills ยอดนิยม

| Skill | ติดตั้ง |
|-------|---------|
| React/Next.js optimization | `npx skills add vercel/vercel-react-best-practices` |
| Web design patterns | `npx skills add ibelick/web-design-guidelines` |
| Frontend UI/UX | `npx skills add ibelick/frontend-design` |
| TypeScript best practices | `npx skills find typescript` |

---

## Resources

- เว็บไซต์: https://skills.sh
- GitHub: https://github.com/vercel-labs/skills
