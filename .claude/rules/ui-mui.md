# MUI (Material UI)

## Overview
React Component Library ที่ใช้ Material Design จาก Google

---

## Installation

```bash
# Core
npm install @mui/material @emotion/react @emotion/styled

# Icons (optional)
npm install @mui/icons-material
```

---

## Next.js App Router Setup

```tsx
// app/layout.tsx
import { AppRouterCacheProvider } from '@mui/material-nextjs/v14-appRouter';
import { ThemeProvider } from '@mui/material/styles';
import CssBaseline from '@mui/material/CssBaseline';
import theme from './theme';

export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body>
        <AppRouterCacheProvider>
          <ThemeProvider theme={theme}>
            <CssBaseline />
            {children}
          </ThemeProvider>
        </AppRouterCacheProvider>
      </body>
    </html>
  );
}
```

```bash
# Next.js integration
npm install @mui/material-nextjs
```

---

## Theme Customization

```tsx
// theme.ts
import { createTheme } from '@mui/material/styles';

const theme = createTheme({
  palette: {
    primary: {
      main: '#1976d2',
    },
    secondary: {
      main: '#dc004e',
    },
  },
  typography: {
    fontFamily: '"Inter", "Roboto", "Helvetica", "Arial", sans-serif',
  },
  components: {
    MuiButton: {
      styleOverrides: {
        root: {
          textTransform: 'none', // ไม่ uppercase
          borderRadius: 8,
        },
      },
    },
  },
});

export default theme;
```

---

## Common Components

### Button
```tsx
import Button from '@mui/material/Button';

<Button variant="contained">Primary</Button>
<Button variant="outlined">Outlined</Button>
<Button variant="text">Text</Button>
<Button variant="contained" color="secondary">Secondary</Button>
<Button variant="contained" disabled>Disabled</Button>
<Button variant="contained" startIcon={<SaveIcon />}>Save</Button>
```

### TextField
```tsx
import TextField from '@mui/material/TextField';

<TextField label="Name" variant="outlined" />
<TextField label="Email" variant="filled" />
<TextField label="Password" type="password" />
<TextField label="Error" error helperText="Invalid input" />
<TextField label="Multiline" multiline rows={4} />
```

### Card
```tsx
import Card from '@mui/material/Card';
import CardContent from '@mui/material/CardContent';
import CardActions from '@mui/material/CardActions';
import Typography from '@mui/material/Typography';

<Card>
  <CardContent>
    <Typography variant="h5">Card Title</Typography>
    <Typography variant="body2" color="text.secondary">
      Card content goes here.
    </Typography>
  </CardContent>
  <CardActions>
    <Button size="small">Learn More</Button>
  </CardActions>
</Card>
```

### AppBar & Navigation
```tsx
import AppBar from '@mui/material/AppBar';
import Toolbar from '@mui/material/Toolbar';
import IconButton from '@mui/material/IconButton';
import MenuIcon from '@mui/icons-material/Menu';

<AppBar position="static">
  <Toolbar>
    <IconButton edge="start" color="inherit">
      <MenuIcon />
    </IconButton>
    <Typography variant="h6" sx={{ flexGrow: 1 }}>
      App Name
    </Typography>
    <Button color="inherit">Login</Button>
  </Toolbar>
</AppBar>
```

---

## Styling with sx prop

```tsx
// sx prop - inline styling
<Box
  sx={{
    width: 300,
    height: 300,
    bgcolor: 'primary.main',
    '&:hover': {
      bgcolor: 'primary.dark',
    },
    p: 2,        // padding: 16px
    m: 1,        // margin: 8px
    borderRadius: 2,
  }}
/>
```

### Spacing Scale
| Value | Pixels |
|-------|--------|
| 1 | 8px |
| 2 | 16px |
| 3 | 24px |
| 4 | 32px |

---

## Grid Layout

```tsx
import Grid from '@mui/material/Grid';

<Grid container spacing={2}>
  <Grid item xs={12} md={6}>
    <Item>xs=12 md=6</Item>
  </Grid>
  <Grid item xs={12} md={6}>
    <Item>xs=12 md=6</Item>
  </Grid>
</Grid>
```

---

## Icons

```tsx
import HomeIcon from '@mui/icons-material/Home';
import DeleteIcon from '@mui/icons-material/Delete';
import SearchIcon from '@mui/icons-material/Search';

<HomeIcon />
<HomeIcon color="primary" />
<HomeIcon fontSize="large" />
<DeleteIcon color="error" />
```

---

## Best Practices

### 1. Import แยก component
```tsx
// ✅ Good - tree shaking
import Button from '@mui/material/Button';
import TextField from '@mui/material/TextField';

// ❌ Bad - bundle ใหญ่
import { Button, TextField } from '@mui/material';
```

### 2. ใช้ Typography สำหรับ text
```tsx
// ✅ Good
<Typography variant="h1">Heading</Typography>
<Typography variant="body1">Paragraph</Typography>

// ❌ Bad
<h1>Heading</h1>
<p>Paragraph</p>
```

### 3. ใช้ Box แทน div
```tsx
// ✅ Good - ใช้ sx prop ได้
<Box sx={{ p: 2, bgcolor: 'grey.100' }}>Content</Box>

// ❌ Less ideal
<div style={{ padding: 16 }}>Content</div>
```

---

## Dark Mode

```tsx
import { createTheme, ThemeProvider } from '@mui/material/styles';
import useMediaQuery from '@mui/material/useMediaQuery';

function App() {
  const prefersDarkMode = useMediaQuery('(prefers-color-scheme: dark)');

  const theme = createTheme({
    palette: {
      mode: prefersDarkMode ? 'dark' : 'light',
    },
  });

  return (
    <ThemeProvider theme={theme}>
      <CssBaseline />
      <App />
    </ThemeProvider>
  );
}
```

---

## Resources

- Docs: https://mui.com/material-ui/
- Components: https://mui.com/material-ui/all-components/
- Icons: https://mui.com/material-ui/material-icons/
