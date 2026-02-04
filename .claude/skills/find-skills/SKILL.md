---
name: find-skills
description: ค้นหาและติดตั้ง Agent Skills จาก skills.sh
user-invocable: true
---

# Find Skills - ค้นหา Agent Skills

## เมื่อ user พิมพ์ /find-skills

### ขั้นตอนที่ 1: ถาม user ว่าต้องการอะไร

ถามว่า:
- ต้องการ skill เกี่ยวกับอะไร?
- หรือต้องการดู skill ยอดนิยม?

### ขั้นตอนที่ 2: ค้นหา skill

**ถ้า user บอกว่าต้องการอะไร:**
```bash
npx skills find [keyword]
```

ตัวอย่าง:
- "React performance" → `npx skills find react performance`
- "testing" → `npx skills find testing`
- "SEO" → `npx skills find seo`

**ถ้า user อยากดู skill ยอดนิยม:**

แนะนำ Top 10 จาก skills.sh:

| Skill | ประโยชน์ | ติดตั้ง |
|-------|---------|---------|
| `vercel-labs/skills/find-skills` | ค้นหา skills อัตโนมัติ | `npx skills add vercel-labs/skills/find-skills` |
| `vercel/vercel-react-best-practices` | React/Next.js optimization | `npx skills add vercel/vercel-react-best-practices` |
| `ibelick/web-design-guidelines` | Web design patterns | `npx skills add ibelick/web-design-guidelines` |
| `remotion-dev/remotion-best-practices` | Video library | `npx skills add remotion-dev/remotion-best-practices` |
| `ibelick/frontend-design` | UI/UX guidance | `npx skills add ibelick/frontend-design` |

### ขั้นตอนที่ 3: ช่วยติดตั้ง

เมื่อ user เลือก skill แล้ว ช่วยรันคำสั่ง:

```bash
npx skills add <owner/repo>
```

Options:
- `-g` หรือ `--global` = ติดตั้งแบบ global (ใช้ได้ทุก project)
- `-y` หรือ `--yes` = ไม่ต้องถามยืนยัน

### ขั้นตอนที่ 4: อธิบายการใช้งาน

หลังติดตั้งเสร็จ:
1. บอก user ว่า skill ถูกติดตั้งที่ไหน (`.agents/` folder)
2. อธิบายวิธีใช้ skill ที่ติดตั้ง
3. แนะนำให้ลองใช้งานทันที

---

## Quick Commands

```bash
# ค้นหา skill
npx skills find [keyword]

# ติดตั้ง skill
npx skills add <owner/repo>

# ติดตั้งแบบ global
npx skills add -g <owner/repo>

# ดู skills ที่ติดตั้งแล้ว
npx skills list

# อัพเดท skills
npx skills update
```

---

## แนะนำ: ติดตั้ง find-skills skill

ถ้า user ยังไม่มี find-skills skill จาก Vercel แนะนำให้ติดตั้ง:

```bash
npx skills add vercel-labs/skills/find-skills
```

ประโยชน์: หลังติดตั้งแล้ว AI จะค้นหา skills ให้อัตโนมัติเมื่อถามว่า "มี skill สำหรับ X ไหม?"

---

## Resources

- เว็บไซต์: https://skills.sh
- GitHub: https://github.com/vercel-labs/skills
