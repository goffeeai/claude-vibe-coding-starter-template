# Key Decisions Log

> บันทึกการตัดสินใจสำคัญของโปรเจค เพื่อให้ AI เข้าใจ context และไม่ถามซ้ำ

## Tech Stack Decisions

### Frontend
| ตัดสินใจ | เหตุผล |
|---------|--------|
| ใช้ React | ... |
| ใช้ Tailwind CSS | ... |
| ใช้ Zustand | ... |

### Backend
| ตัดสินใจ | เหตุผล |
|---------|--------|
| ใช้ Express | ... |
| ใช้ PostgreSQL | ... |

### Deployment
| ตัดสินใจ | เหตุผล |
|---------|--------|
| Deploy ที่ Vercel | ... |

---

## Architecture Decisions

### ทำไมใช้โครงสร้างแบบนี้?
- ...

### ทำไมแยก services ออกมา?
- ...

---

## Naming Conventions

### ทำไมตั้งชื่อแบบนี้?
- Components: PascalCase เพราะ...
- Files: kebab-case เพราะ...

---

## ข้อตกลงอื่นๆ

### Code Style
- ใช้ single quotes
- ใช้ semicolons
- Indent 2 spaces

### Git
- Commit message ภาษาอังกฤษ
- Branch naming: `feature/xxx`, `fix/xxx`

---

## สิ่งที่ห้ามทำ (Don'ts)

- ❌ ห้ามใช้ `any` ใน TypeScript
- ❌ ห้าม commit `.env` files
- ❌ ห้ามใช้ inline styles (ใช้ Tailwind แทน)

---

*อัพเดทไฟล์นี้เมื่อมีการตัดสินใจสำคัญใหม่*
