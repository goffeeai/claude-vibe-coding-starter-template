# Skills Guide

## Skills คืออะไร?

Skills คือ slash commands ที่คุณสามารถเรียกใช้ใน Claude Code เช่น `/start`, `/save`

---

## Skills ที่มี

### /start
เริ่มต้นทำงานกับโปรเจค

**ใช้เมื่อ:**
- เปิดโปรเจคใหม่
- กลับมาทำต่อ
- ต้องการทำความเข้าใจ codebase

**AI จะถาม:**
1. นี่คือโปรเจคใหม่หรือมีอยู่แล้ว?
2. ต้องการทำอะไร?
3. มี requirements อะไรบ้าง?

---

### /save
บันทึก context (ไม่ push GitHub)

**ใช้เมื่อ:**
- เห็น context ใกล้เต็ม
- ต้องการพักโปรเจค
- บันทึกงานไว้ทำต่อ

**AI จะทำ:**
1. สรุปสิ่งที่ทำไป
2. บันทึกลง changelog
3. อัพเดท overview
4. Commit (local เท่านั้น)

**หมายเหตุ:** ไม่ push ขึ้น GitHub

---

### /save-github
บันทึก context + push GitHub

**ใช้เมื่อ:**
- ต้องการบันทึกและ backup ขึ้น GitHub
- จะย้ายไปทำเครื่องอื่น
- ทำงานเป็นทีม ต้องแชร์โค้ด

**AI จะทำ:**
1. สรุปสิ่งที่ทำไป
2. บันทึกลง changelog
3. Commit และ push
4. ถ้ายังไม่มี repo จะถาม Private/Public

---

### /github
Push ขึ้น GitHub อย่างเดียว

**ใช้เมื่อ:**
- ต้องการ push โค้ดขึ้น GitHub
- สร้าง repo ใหม่บน GitHub

**AI จะทำ:**
1. ตรวจสอบว่ามี repo หรือยัง
2. ถ้ายังไม่มี → ถาม Private/Public
3. Push ขึ้น GitHub

---

### /help-me
ขอความช่วยเหลือแบบเป็นมิตร

**ใช้เมื่อ:**
- ไม่เข้าใจ error
- ไม่รู้จะเริ่มตรงไหน
- ต้องการคำแนะนำ

**AI จะ:**
1. ถามให้ชัดเจน
2. อธิบายง่ายๆ
3. ให้ตัวอย่าง
4. แนะนำขั้นตอนถัดไป

---

### /show-creds
แสดง credentials ของโปรเจค

**ใช้เมื่อ:**
- ลืม password
- ต้องการดู API keys
- เช็ค connection strings

**AI จะแสดง:**
- Database credentials
- API keys
- Server IPs
- Service URLs

---

### /test
รัน tests และ auto-fix ถ้ามีปัญหา

**ใช้เมื่อ:**
- เขียน feature เสร็จ ต้องการทดสอบ
- แก้ bug แล้วต้องการตรวจสอบ
- ก่อน commit/push ขึ้น GitHub

**AI จะทำ:**
1. ตรวจจับ test framework (Jest, Vitest, Playwright, Cypress, pytest)
2. รัน tests ที่มีในโปรเจค
3. ถ้า fail → วิเคราะห์และแก้ไขอัตโนมัติ (สูงสุด 3 รอบ)
4. สรุปผลให้ทราบ

**Test frameworks ที่รองรับ:**
- Playwright (E2E)
- Jest (Unit)
- Vitest (Unit)
- Cypress (E2E)
- pytest (Python)

**หมายเหตุ:** ถ้าไม่มี test framework จะถามว่าต้องการติดตั้งไหม

---

## เปรียบเทียบ Save Skills

| Feature | /save | /save-github | /github |
|---------|-------|--------------|---------|
| บันทึก changelog | ✅ | ✅ | ❌ |
| Commit local | ✅ | ✅ | ✅* |
| Push GitHub | ❌ | ✅ | ✅ |
| สร้าง repo ใหม่ | ❌ | ✅ | ✅ |

*ถ้ามี uncommitted changes จะถามก่อน

---

## เมื่อไหร่ใช้อะไร?

```
ทำงานอยู่คนเดียว, ยังไม่อยาก push
→ /save

ทำเสร็จแล้ว, อยาก backup ขึ้น GitHub
→ /save-github

แค่อยาก push โค้ดขึ้น GitHub
→ /github
```

---

## วิธีสร้าง Skill ใหม่

### 1. สร้างโฟลเดอร์
```bash
mkdir -p .claude/skills/my-skill
```

### 2. สร้าง SKILL.md
```markdown
# My Custom Skill

## Description
อธิบายว่า skill นี้ทำอะไร

## Instructions
คำสั่งที่ AI ต้องทำ:
1. ขั้นตอนที่ 1
2. ขั้นตอนที่ 2
3. ขั้นตอนที่ 3

## Output
ผลลัพธ์ที่คาดหวัง
```

### 3. ใช้งาน
```
/my-skill
```

---

## ตัวอย่าง: สร้าง Skill สำหรับ Deploy

`.claude/skills/deploy/SKILL.md`:

```markdown
# Deploy Skill

## Description
Deploy โปรเจคขึ้น production server

## Pre-requisites
- ต้อง build สำเร็จก่อน
- ต้องมี SSH access

## Instructions
1. ถามว่าจะ deploy ไป server ไหน
2. รัน build command
3. Copy files ไป server
4. Restart service
5. ตรวจสอบว่า deploy สำเร็จ

## Commands
- Build: `npm run build`
- Deploy: `scp -r dist/* user@server:/var/www/app/`
- Restart: `ssh user@server "pm2 restart app"`
```
