# Zustand - State Management

## Overview
Lightweight state management สำหรับ React - ง่ายกว่า Redux มาก

## Installation
```bash
npm install zustand
```

## Basic Store

```typescript
// stores/useCounterStore.ts
import { create } from 'zustand'

interface CounterState {
  count: number
  increment: () => void
  decrement: () => void
  reset: () => void
}

export const useCounterStore = create<CounterState>((set) => ({
  count: 0,
  increment: () => set((state) => ({ count: state.count + 1 })),
  decrement: () => set((state) => ({ count: state.count - 1 })),
  reset: () => set({ count: 0 }),
}))
```

## Usage in Component

```tsx
import { useCounterStore } from '@/stores/useCounterStore'

function Counter() {
  const { count, increment, decrement, reset } = useCounterStore()

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>+</button>
      <button onClick={decrement}>-</button>
      <button onClick={reset}>Reset</button>
    </div>
  )
}
```

## Async Actions

```typescript
// stores/useUserStore.ts
import { create } from 'zustand'

interface User {
  id: string
  name: string
  email: string
}

interface UserState {
  user: User | null
  loading: boolean
  error: string | null
  fetchUser: (id: string) => Promise<void>
  logout: () => void
}

export const useUserStore = create<UserState>((set) => ({
  user: null,
  loading: false,
  error: null,

  fetchUser: async (id) => {
    set({ loading: true, error: null })
    try {
      const res = await fetch(`/api/users/${id}`)
      const user = await res.json()
      set({ user, loading: false })
    } catch (error) {
      set({ error: 'Failed to fetch user', loading: false })
    }
  },

  logout: () => set({ user: null }),
}))
```

## Persist State (localStorage)

```typescript
import { create } from 'zustand'
import { persist } from 'zustand/middleware'

interface SettingsState {
  theme: 'light' | 'dark'
  language: string
  setTheme: (theme: 'light' | 'dark') => void
  setLanguage: (lang: string) => void
}

export const useSettingsStore = create<SettingsState>()(
  persist(
    (set) => ({
      theme: 'light',
      language: 'th',
      setTheme: (theme) => set({ theme }),
      setLanguage: (language) => set({ language }),
    }),
    {
      name: 'settings-storage', // localStorage key
    }
  )
)
```

## Selectors (Performance)

```tsx
// เลือกเฉพาะ field ที่ต้องการ (ป้องกัน re-render)
const count = useCounterStore((state) => state.count)
const increment = useCounterStore((state) => state.increment)

// หรือใช้ shallow compare
import { shallow } from 'zustand/shallow'

const { count, increment } = useCounterStore(
  (state) => ({ count: state.count, increment: state.increment }),
  shallow
)
```

## DevTools

```typescript
import { create } from 'zustand'
import { devtools } from 'zustand/middleware'

export const useStore = create<State>()(
  devtools(
    (set) => ({
      // ...
    }),
    { name: 'MyStore' }
  )
)
```

## Project Structure

```
src/
├── stores/
│   ├── useAuthStore.ts      # Auth state
│   ├── useCartStore.ts      # Shopping cart
│   ├── useUIStore.ts        # UI state (modals, sidebar)
│   └── useSettingsStore.ts  # User preferences
```

## Best Practices

1. **แยก store ตาม feature** - ไม่ต้องรวมทุกอย่างใน store เดียว
2. **ใช้ selectors** - เลือกเฉพาะ state ที่ต้องการ
3. **Persist เฉพาะที่จำเป็น** - อย่า persist ทุกอย่าง
4. **ตั้งชื่อ store ด้วย use** - เช่น `useCartStore`

## Zustand vs Redux

| Feature | Zustand | Redux |
|---------|---------|-------|
| Boilerplate | น้อยมาก | เยอะ |
| Learning curve | ง่าย | ยาก |
| Bundle size | ~1KB | ~7KB |
| DevTools | รองรับ | รองรับ |
| Middleware | มี | มี |

## Links
- [Zustand Docs](https://docs.pmnd.rs/zustand)
- [GitHub](https://github.com/pmndrs/zustand)
