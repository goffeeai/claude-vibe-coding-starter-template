# Changelog Guide

## ทำไมต้องเขียน Changelog?

1. **AI จำได้** - เมื่อ context reset จะรู้ว่าทำอะไรไปแล้ว
2. **Track progress** - ดูความคืบหน้าของโปรเจค
3. **Team collaboration** - ทีมรู้ว่าใครทำอะไร
4. **Debugging** - รู้ว่าอะไรเปลี่ยนเมื่อไหร่

---

## Format

```markdown
# Changelog

## [วันที่] - [หัวข้อสั้นๆ]

### Added
- Feature ใหม่ที่เพิ่ม

### Changed
- สิ่งที่แก้ไข

### Fixed
- Bug ที่แก้

### Removed
- สิ่งที่ลบออก

### Notes
- หมายเหตุหรือสิ่งที่ต้องทำต่อ
```

---

## ตัวอย่าง

```markdown
# Changelog

## 2024-01-20 - User Authentication

### Added
- Login page with email/password
- Logout functionality
- Protected routes middleware
- Session management with cookies

### Changed
- Updated navbar to show user info
- API routes now require authentication

### Fixed
- Fixed CORS issue with API calls

### Notes
- TODO: Add forgot password feature
- TODO: Add social login (Google, GitHub)

---

## 2024-01-18 - Initial Setup

### Added
- Next.js 14 project with App Router
- Tailwind CSS + Shadcn/ui setup
- PostgreSQL + Prisma configuration
- Basic folder structure

### Notes
- Development server: http://localhost:3000
- Database: Supabase PostgreSQL
```

---

## เมื่อไหร่ควรเขียน?

### ต้องเขียน
- เพิ่ม feature ใหม่
- แก้ bug สำคัญ
- เปลี่ยน database schema
- เปลี่ยน API structure
- Deploy ขึ้น production

### ไม่ต้องเขียน
- แก้ typo
- ปรับ CSS เล็กน้อย
- Refactor เล็กน้อย
- Update dependencies

---

## Tips

1. **เขียนทันที** - อย่ารอ จะลืม
2. **สั้น กระชับ** - ไม่ต้องละเอียดมาก
3. **ใช้ /save หรือ /save-github** - AI จะช่วยเขียนให้
4. **Link to commits** - ถ้ามี git commit ที่เกี่ยวข้อง

---

## Integration กับ Save Skills

### /save (บันทึก local)
เมื่อใช้ `/save` AI จะ:
1. สรุปสิ่งที่ทำในเซสชันนี้
2. เพิ่มลง `09-changelog.md` อัตโนมัติ
3. Commit (local เท่านั้น ไม่ push)

### /save-github (บันทึก + push)
เมื่อใช้ `/save-github` AI จะ:
1. สรุปสิ่งที่ทำในเซสชันนี้
2. เพิ่มลง `09-changelog.md` อัตโนมัติ
3. Commit และ push ขึ้น GitHub

---

## ตัวอย่าง prompt

```
/save

AI: สรุปสิ่งที่ทำในเซสชันนี้:

## 2024-01-20 - Product CRUD

### Added
- Product listing page
- Add product form
- Edit product modal
- Delete confirmation dialog

### Changed
- Updated sidebar navigation

✅ บันทึกเรียบร้อยแล้ว (local)

💡 ต้องการ push ขึ้น GitHub ด้วยไหม?
   ใช้ /github หรือ /save-github
```
