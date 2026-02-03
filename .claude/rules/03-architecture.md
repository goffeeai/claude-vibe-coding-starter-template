# Project Architecture

> AI ต้องอ่านไฟล์นี้เพื่อเข้าใจโครงสร้างโปรเจค ก่อนแก้ไขไฟล์ใดๆ

## โครงสร้างโฟลเดอร์

```
project-name/
├── src/                    # Source code หลัก
│   ├── components/         # React/Vue components
│   ├── pages/              # Pages/Routes
│   ├── hooks/              # Custom hooks
│   ├── utils/              # Utility functions
│   ├── services/           # API calls
│   ├── stores/             # State management (Zustand/Redux)
│   └── types/              # TypeScript types
├── public/                 # Static files
├── tests/                  # Test files
└── ...
```

## ไฟล์สำคัญ

| ไฟล์ | หน้าที่ |
|------|--------|
| `src/App.tsx` | Entry point หลัก |
| `src/pages/index.tsx` | หน้าแรก |
| `src/components/Layout.tsx` | Layout wrapper |
| ... | ... |

## Flow หลัก

```
User → Pages → Components → Services → API
                    ↓
                 Stores (State)
```

## Naming Conventions

- **Components**: PascalCase (`UserCard.tsx`)
- **Hooks**: camelCase with `use` prefix (`useAuth.ts`)
- **Utils**: camelCase (`formatDate.ts`)
- **Types**: PascalCase with `I` or `T` prefix (`IUser.ts`)

## หมายเหตุสำหรับ AI

- ถ้าไม่แน่ใจว่าไฟล์อยู่ที่ไหน → ถาม user ก่อน
- ถ้าต้องสร้างไฟล์ใหม่ → ดูโครงสร้างนี้ก่อน
- อย่าสร้างโฟลเดอร์ใหม่โดยไม่จำเป็น

---

*อัพเดทไฟล์นี้เมื่อโครงสร้างเปลี่ยน*
