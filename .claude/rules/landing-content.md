# Landing Page Content Structure

## Overview
Best practices for landing page content organization

---

## Page Sections

### 1. Hero Section
```html
<section class="hero">
  <h1>Main Value Proposition</h1>
  <p class="subtitle">Supporting statement that explains the benefit</p>
  <a href="#cta" class="btn-primary">Call to Action</a>
</section>
```

**Tips:**
- H1 ควรมีแค่ 1 ตัวต่อหน้า
- ใช้คำที่ชัดเจน บอกประโยชน์
- CTA button ควรโดดเด่น

---

### 2. Features/Benefits
```html
<section class="features">
  <h2>Why Choose Us</h2>

  <div class="feature-grid">
    <div class="feature">
      <img src="icon-fast.svg" alt="" />
      <h3>Fast</h3>
      <p>Description of this feature</p>
    </div>

    <div class="feature">
      <img src="icon-secure.svg" alt="" />
      <h3>Secure</h3>
      <p>Description of this feature</p>
    </div>

    <div class="feature">
      <img src="icon-easy.svg" alt="" />
      <h3>Easy</h3>
      <p>Description of this feature</p>
    </div>
  </div>
</section>
```

---

### 3. Social Proof
```html
<section class="testimonials">
  <h2>What Our Customers Say</h2>

  <blockquote>
    <p>"Great product! Changed my life."</p>
    <cite>
      <img src="avatar.jpg" alt="" />
      <strong>John Doe</strong>
      <span>CEO, Company</span>
    </cite>
  </blockquote>
</section>

<section class="logos">
  <h2>Trusted by</h2>
  <div class="logo-grid">
    <img src="logo1.svg" alt="Company 1" />
    <img src="logo2.svg" alt="Company 2" />
  </div>
</section>
```

---

### 4. Pricing
```html
<section class="pricing">
  <h2>Simple Pricing</h2>

  <div class="pricing-grid">
    <div class="plan">
      <h3>Basic</h3>
      <p class="price">$9<span>/month</span></p>
      <ul>
        <li>Feature 1</li>
        <li>Feature 2</li>
      </ul>
      <a href="#" class="btn">Get Started</a>
    </div>

    <div class="plan featured">
      <span class="badge">Popular</span>
      <h3>Pro</h3>
      <p class="price">$29<span>/month</span></p>
      <ul>
        <li>Everything in Basic</li>
        <li>Feature 3</li>
        <li>Feature 4</li>
      </ul>
      <a href="#" class="btn-primary">Get Started</a>
    </div>
  </div>
</section>
```

---

### 5. FAQ
```html
<section class="faq">
  <h2>Frequently Asked Questions</h2>

  <details>
    <summary>Question 1?</summary>
    <p>Answer to question 1...</p>
  </details>

  <details>
    <summary>Question 2?</summary>
    <p>Answer to question 2...</p>
  </details>
</section>
```

---

### 6. Final CTA
```html
<section class="cta-section">
  <h2>Ready to Get Started?</h2>
  <p>Join thousands of happy customers</p>
  <a href="#" class="btn-primary btn-large">Start Free Trial</a>
</section>
```

---

## Content Tips

### Headlines
- ใช้ตัวเลข: "5 Ways to..."
- ถามคำถาม: "Tired of...?"
- บอกประโยชน์: "Save 10 hours/week"

### Copy
- ใช้ "you" แทน "we"
- เน้น benefits ไม่ใช่ features
- ใช้ bullet points
- Keep it simple

### CTA Buttons
- ใช้ action words: "Get", "Start", "Try"
- เพิ่ม urgency: "Get Started Free"
- ทำให้โดดเด่น

---

## Page Flow

```
Hero (Value Proposition)
         ↓
Features (What you get)
         ↓
Social Proof (Trust)
         ↓
Pricing (Make decision)
         ↓
FAQ (Remove objections)
         ↓
Final CTA (Take action)
```
