# Playwright - E2E Testing

## Overview
End-to-End testing framework จาก Microsoft - รองรับ Chrome, Firefox, Safari

## Installation
```bash
npm init playwright@latest
```

เลือก:
- TypeScript
- tests folder
- GitHub Actions workflow (optional)
- Install browsers

## Project Structure

```
project/
├── tests/
│   ├── auth.spec.ts       # Authentication tests
│   ├── home.spec.ts       # Homepage tests
│   └── checkout.spec.ts   # Checkout flow tests
├── playwright.config.ts   # Configuration
└── package.json
```

## Basic Test

```typescript
// tests/home.spec.ts
import { test, expect } from '@playwright/test'

test('homepage has title', async ({ page }) => {
  await page.goto('/')
  await expect(page).toHaveTitle(/My App/)
})

test('can navigate to about page', async ({ page }) => {
  await page.goto('/')
  await page.click('text=About')
  await expect(page).toHaveURL('/about')
})
```

## Common Actions

```typescript
// Navigation
await page.goto('https://example.com')
await page.goBack()
await page.goForward()
await page.reload()

// Click
await page.click('button')
await page.click('text=Submit')
await page.click('#submit-btn')
await page.click('[data-testid="submit"]')

// Fill input
await page.fill('input[name="email"]', 'test@example.com')
await page.fill('#password', 'secret123')

// Select dropdown
await page.selectOption('select#country', 'Thailand')

// Check/Uncheck
await page.check('input[type="checkbox"]')
await page.uncheck('input[type="checkbox"]')

// Upload file
await page.setInputFiles('input[type="file"]', 'path/to/file.pdf')

// Wait
await page.waitForSelector('.loading', { state: 'hidden' })
await page.waitForURL('/dashboard')
await page.waitForResponse('/api/users')
```

## Assertions

```typescript
// Page
await expect(page).toHaveTitle('My App')
await expect(page).toHaveURL('/dashboard')

// Element
const button = page.locator('button')
await expect(button).toBeVisible()
await expect(button).toBeEnabled()
await expect(button).toBeDisabled()
await expect(button).toHaveText('Submit')
await expect(button).toHaveClass('btn-primary')

// Input
const input = page.locator('input[name="email"]')
await expect(input).toHaveValue('test@example.com')
await expect(input).toBeFocused()

// List
const items = page.locator('.list-item')
await expect(items).toHaveCount(5)
```

## Authentication Test

```typescript
// tests/auth.spec.ts
import { test, expect } from '@playwright/test'

test.describe('Authentication', () => {
  test('can login with valid credentials', async ({ page }) => {
    await page.goto('/login')

    await page.fill('input[name="email"]', 'user@example.com')
    await page.fill('input[name="password"]', 'password123')
    await page.click('button[type="submit"]')

    await expect(page).toHaveURL('/dashboard')
    await expect(page.locator('text=Welcome')).toBeVisible()
  })

  test('shows error with invalid credentials', async ({ page }) => {
    await page.goto('/login')

    await page.fill('input[name="email"]', 'wrong@example.com')
    await page.fill('input[name="password"]', 'wrongpass')
    await page.click('button[type="submit"]')

    await expect(page.locator('.error-message')).toHaveText('Invalid credentials')
  })
})
```

## Page Object Model

```typescript
// pages/LoginPage.ts
import { Page, Locator } from '@playwright/test'

export class LoginPage {
  readonly page: Page
  readonly emailInput: Locator
  readonly passwordInput: Locator
  readonly submitButton: Locator
  readonly errorMessage: Locator

  constructor(page: Page) {
    this.page = page
    this.emailInput = page.locator('input[name="email"]')
    this.passwordInput = page.locator('input[name="password"]')
    this.submitButton = page.locator('button[type="submit"]')
    this.errorMessage = page.locator('.error-message')
  }

  async goto() {
    await this.page.goto('/login')
  }

  async login(email: string, password: string) {
    await this.emailInput.fill(email)
    await this.passwordInput.fill(password)
    await this.submitButton.click()
  }
}

// tests/auth.spec.ts
import { test, expect } from '@playwright/test'
import { LoginPage } from '../pages/LoginPage'

test('can login', async ({ page }) => {
  const loginPage = new LoginPage(page)
  await loginPage.goto()
  await loginPage.login('user@example.com', 'password123')
  await expect(page).toHaveURL('/dashboard')
})
```

## Configuration

```typescript
// playwright.config.ts
import { defineConfig, devices } from '@playwright/test'

export default defineConfig({
  testDir: './tests',
  timeout: 30000,
  retries: 2,

  use: {
    baseURL: 'http://localhost:3000',
    screenshot: 'only-on-failure',
    video: 'retain-on-failure',
    trace: 'retain-on-failure',
  },

  projects: [
    { name: 'chromium', use: { ...devices['Desktop Chrome'] } },
    { name: 'firefox', use: { ...devices['Desktop Firefox'] } },
    { name: 'webkit', use: { ...devices['Desktop Safari'] } },
    { name: 'mobile', use: { ...devices['iPhone 13'] } },
  ],

  webServer: {
    command: 'npm run dev',
    port: 3000,
    reuseExistingServer: !process.env.CI,
  },
})
```

## Commands

```bash
# Run all tests
npx playwright test

# Run specific file
npx playwright test tests/auth.spec.ts

# Run in headed mode (see browser)
npx playwright test --headed

# Run specific browser
npx playwright test --project=chromium

# Debug mode
npx playwright test --debug

# Generate test code (UI mode)
npx playwright codegen http://localhost:3000

# View report
npx playwright show-report
```

## CI/CD (GitHub Actions)

```yaml
# .github/workflows/playwright.yml
name: Playwright Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm ci
      - run: npx playwright install --with-deps
      - run: npx playwright test
      - uses: actions/upload-artifact@v4
        if: failure()
        with:
          name: playwright-report
          path: playwright-report/
```

## Best Practices

1. **ใช้ data-testid** - `[data-testid="submit-btn"]` ดีกว่า `.btn-primary`
2. **Page Object Model** - แยก locators ออกมา reuse ได้
3. **Test isolation** - แต่ละ test ควร independent
4. **Visual testing** - ใช้ screenshot comparison
5. **Parallel tests** - Playwright รัน parallel by default

## Links
- [Playwright Docs](https://playwright.dev/)
- [Best Practices](https://playwright.dev/docs/best-practices)
- [Test Generator](https://playwright.dev/docs/codegen)
