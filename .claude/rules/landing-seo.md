# SEO / AEO / AI Mode

## Overview
Optimization for Search Engines, Answer Engines, and AI

---

## SEO Basics

### Meta Tags
```html
<head>
  <title>Page Title - Brand Name</title>
  <meta name="description" content="Description 150-160 chars" />
  <meta name="keywords" content="keyword1, keyword2" />
  <link rel="canonical" href="https://example.com/page" />
</head>
```

### Open Graph (Facebook)
```html
<meta property="og:title" content="Title" />
<meta property="og:description" content="Description" />
<meta property="og:image" content="https://example.com/image.jpg" />
<meta property="og:url" content="https://example.com/page" />
<meta property="og:type" content="website" />
```

### Twitter Card
```html
<meta name="twitter:card" content="summary_large_image" />
<meta name="twitter:title" content="Title" />
<meta name="twitter:description" content="Description" />
<meta name="twitter:image" content="https://example.com/image.jpg" />
```

---

## Structured Data (Schema.org)

### Organization
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "Company Name",
  "url": "https://example.com",
  "logo": "https://example.com/logo.png",
  "sameAs": [
    "https://facebook.com/company",
    "https://twitter.com/company"
  ]
}
</script>
```

### Article/Blog Post
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

### FAQ
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [{
    "@type": "Question",
    "name": "Question 1?",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "Answer 1"
    }
  }]
}
</script>
```

---

## AEO (Answer Engine Optimization)

เพื่อให้ AI/LLM เข้าใจ content:

### 1. Clear Structure
```html
<article>
  <h1>Main Topic</h1>
  <p>Brief introduction answering the main question.</p>

  <h2>Subtopic 1</h2>
  <p>Detailed explanation...</p>

  <h2>Subtopic 2</h2>
  <p>Detailed explanation...</p>
</article>
```

### 2. FAQ Format
```html
<section class="faq">
  <h2>Frequently Asked Questions</h2>

  <details>
    <summary>What is X?</summary>
    <p>X is...</p>
  </details>

  <details>
    <summary>How does X work?</summary>
    <p>X works by...</p>
  </details>
</section>
```

### 3. Definition Lists
```html
<dl>
  <dt>Term 1</dt>
  <dd>Definition of term 1</dd>

  <dt>Term 2</dt>
  <dd>Definition of term 2</dd>
</dl>
```

---

## Technical SEO

### robots.txt
```
User-agent: *
Allow: /
Disallow: /admin/
Disallow: /api/

Sitemap: https://example.com/sitemap.xml
```

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

---

## Performance (Core Web Vitals)

### LCP (Largest Contentful Paint)
- ใช้ `loading="eager"` สำหรับ hero image
- Preload critical resources

### CLS (Cumulative Layout Shift)
- กำหนด width/height ให้ images
- Reserve space สำหรับ dynamic content

### FID/INP (Interaction)
- Minimize JavaScript
- Use lazy loading

```html
<!-- Preload critical resources -->
<link rel="preload" href="/font.woff2" as="font" crossorigin />
<link rel="preload" href="/hero.jpg" as="image" />

<!-- Lazy load images -->
<img src="image.jpg" loading="lazy" width="800" height="600" alt="Description" />
```
