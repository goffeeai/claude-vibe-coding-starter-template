# React

## Overview
JavaScript library for building user interfaces

## Create Project

```bash
npm create vite@latest my-app -- --template react-ts
cd my-app
npm install
npm run dev
```

---

## Project Structure

```
src/
├── components/
│   ├── Button.tsx
│   └── Card.tsx
├── pages/
│   ├── Home.tsx
│   └── About.tsx
├── hooks/
│   └── useAuth.ts
├── lib/
│   └── api.ts
├── App.tsx
└── main.tsx
```

---

## Components

### Function Component
```tsx
interface ButtonProps {
  children: React.ReactNode;
  onClick?: () => void;
  variant?: 'primary' | 'secondary';
}

function Button({ children, onClick, variant = 'primary' }: ButtonProps) {
  return (
    <button onClick={onClick} className={`btn btn-${variant}`}>
      {children}
    </button>
  );
}

export default Button;
```

---

## Hooks

### useState
```tsx
const [count, setCount] = useState(0);
const [user, setUser] = useState<User | null>(null);
```

### useEffect
```tsx
useEffect(() => {
  fetchData();
}, []); // Run once on mount

useEffect(() => {
  // Run when dependency changes
}, [userId]);
```

### Custom Hook
```tsx
function useAuth() {
  const [user, setUser] = useState<User | null>(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    // Check auth status
  }, []);

  return { user, loading };
}
```

---

## State Management

### Context API
```tsx
const AuthContext = createContext<AuthContextType | null>(null);

export function AuthProvider({ children }: { children: React.ReactNode }) {
  const [user, setUser] = useState<User | null>(null);

  return (
    <AuthContext.Provider value={{ user, setUser }}>
      {children}
    </AuthContext.Provider>
  );
}

export function useAuth() {
  const context = useContext(AuthContext);
  if (!context) throw new Error('useAuth must be used within AuthProvider');
  return context;
}
```

---

## Data Fetching

### With useEffect
```tsx
const [data, setData] = useState<Data | null>(null);
const [loading, setLoading] = useState(true);

useEffect(() => {
  async function fetchData() {
    const response = await fetch('/api/data');
    const data = await response.json();
    setData(data);
    setLoading(false);
  }
  fetchData();
}, []);
```

### With TanStack Query
```tsx
import { useQuery } from '@tanstack/react-query';

const { data, isLoading } = useQuery({
  queryKey: ['users'],
  queryFn: () => fetch('/api/users').then(res => res.json())
});
```

---

## Routing (React Router)

```bash
npm install react-router-dom
```

```tsx
import { BrowserRouter, Routes, Route, Link } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
      </nav>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/users/:id" element={<UserDetail />} />
      </Routes>
    </BrowserRouter>
  );
}
```
