# SEO Basics

## SEO คืออะไร?

SEO (Search Engine Optimization) คือการทำให้เว็บติดอันดับใน Google เพื่อให้คนค้นหาเจอ

---

## 3 Pillars of SEO

### 1. Technical SEO
โครงสร้างเว็บที่ Google เข้าใจ

### 2. On-Page SEO
Content และ HTML ที่ optimize

### 3. Off-Page SEO
Backlinks และ social signals

---

## Technical SEO Checklist

### Meta Tags
```html
<head>
  <title>หัวข้อหน้า | ชื่อเว็บ</title>
  <meta name="description" content="คำอธิบาย 150-160 ตัวอักษร">
  <meta name="robots" content="index, follow">
  <link rel="canonical" href="https://example.com/page">
</head>
```

### Open Graph (Social)
```html
<meta property="og:title" content="หัวข้อ">
<meta property="og:description" content="คำอธิบาย">
<meta property="og:image" content="https://example.com/image.jpg">
<meta property="og:url" content="https://example.com/page">
<meta property="og:type" content="website">
```

### Twitter Card
```html
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="หัวข้อ">
<meta name="twitter:description" content="คำอธิบาย">
<meta name="twitter:image" content="https://example.com/image.jpg">
```

---

## Sitemap & Robots

### sitemap.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://example.com/</loc>
    <lastmod>2024-01-01</lastmod>
    <priority>1.0</priority>
  </url>
  <url>
    <loc>https://example.com/about</loc>
    <lastmod>2024-01-01</lastmod>
    <priority>0.8</priority>
  </url>
</urlset>
```

### robots.txt
```
User-agent: *
Allow: /
Disallow: /admin/
Disallow: /api/

Sitemap: https://example.com/sitemap.xml
```

---

## Structured Data (JSON-LD)

### Organization
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "Company Name",
  "url": "https://example.com",
  "logo": "https://example.com/logo.png"
}
</script>
```

### Article
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "Article Title",
  "author": {
    "@type": "Person",
    "name": "Author Name"
  },
  "datePublished": "2024-01-01",
  "image": "https://example.com/image.jpg"
}
</script>
```

---

## Performance (Core Web Vitals)

### LCP (Largest Contentful Paint)
- เป้าหมาย: < 2.5s
- แก้: Optimize images, preload fonts

### FID (First Input Delay)
- เป้าหมาย: < 100ms
- แก้: Reduce JavaScript, code splitting

### CLS (Cumulative Layout Shift)
- เป้าหมาย: < 0.1
- แก้: Set image dimensions, reserve space

---

## Next.js SEO

```jsx
// app/layout.jsx
export const metadata = {
  title: {
    default: 'My Site',
    template: '%s | My Site',
  },
  description: 'Site description',
  openGraph: {
    title: 'My Site',
    description: 'Site description',
    url: 'https://example.com',
    siteName: 'My Site',
    images: [
      {
        url: 'https://example.com/og.jpg',
        width: 1200,
        height: 630,
      },
    ],
    locale: 'th_TH',
    type: 'website',
  },
};
```

---

## Nuxt.js SEO

```javascript
// nuxt.config.ts
export default defineNuxtConfig({
  app: {
    head: {
      title: 'My Site',
      meta: [
        { name: 'description', content: 'Site description' },
      ],
    },
  },
});
```

```vue
<!-- pages/about.vue -->
<script setup>
useSeoMeta({
  title: 'About',
  description: 'About page description',
  ogTitle: 'About',
  ogDescription: 'About page description',
});
</script>
```

---

## Tools

### Free
- Google Search Console
- Google PageSpeed Insights
- Lighthouse (Chrome DevTools)

### Paid
- Ahrefs
- SEMrush
- Screaming Frog

---

## Quick Wins

1. **Title tags** - ทุกหน้าต้องมี unique title
2. **Meta description** - เขียนให้คนอยากคลิก
3. **Headings** - ใช้ H1-H6 ถูกต้อง
4. **Images** - ใส่ alt text, optimize size
5. **Internal links** - เชื่อมหน้าที่เกี่ยวข้อง
6. **Mobile friendly** - ต้อง responsive
7. **HTTPS** - ต้องมี SSL
8. **Speed** - โหลดเร็ว < 3s
