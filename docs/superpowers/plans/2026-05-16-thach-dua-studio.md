# Thạch Dừa Studio Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a 4-page static website for Thạch Dừa Studio that faithfully clones the Courtney Watts Studio visual design with Thạch Thảo's content.

**Architecture:** Shared `style.css` holds all design tokens, nav, footer, and component styles. Each HTML page links to it and adds no inline styles. A single `carousel.js` handles the testimonials slider on the home page.

**Tech Stack:** Vanilla HTML5, CSS3 (custom properties), vanilla JS — no build tools, no frameworks.

---

## File Map

| File | Action | Responsibility |
|------|--------|---------------|
| `style.css` | Create | Design tokens, reset, typography, nav, footer, all shared components |
| `index.html` | Replace existing | Home: hero, programs preview, testimonials, CTA email strip |
| `programs.html` | Create | Programs: page banner, 3 service cards |
| `about.html` | Create | About: page banner, split bio, secondary image strip |
| `pricing.html` | Create | Pricing: page banner, 2 pricing cards, contact prompt |
| `carousel.js` | Create | Vanilla JS testimonials slider (auto-advance + dot nav) |

---

## Task 1: Create `style.css` — design tokens, reset, typography, nav, footer

**Files:**
- Create: `style.css`

- [ ] **Step 1: Write `style.css`**

```css
/* ── FONTS ── */
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,500;1,400&family=Inter:wght@300;400;500;600&display=swap');

/* ── TOKENS ── */
:root {
  --white:    #ffffff;
  --cream:    #faf7f3;
  --taupe:    #8b704f;
  --charcoal: #1a1a1a;
  --muted:    #888888;
  --border:   #e8e2d9;
}

/* ── RESET ── */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; }
img { display: block; max-width: 100%; }
a { color: inherit; text-decoration: none; }

/* ── BASE ── */
body {
  font-family: 'Inter', ui-sans-serif, system-ui, sans-serif;
  font-weight: 300;
  font-size: 16px;
  line-height: 1.6;
  color: var(--charcoal);
  background: var(--white);
  overflow-x: hidden;
}

/* ── TYPOGRAPHY UTILITIES ── */
.eyebrow {
  font-size: 10px;
  font-weight: 600;
  letter-spacing: 0.26em;
  text-transform: uppercase;
  color: var(--taupe);
  margin-bottom: 10px;
  display: block;
}
.section-title {
  font-family: 'Playfair Display', serif;
  font-size: clamp(28px, 4vw, 44px);
  font-weight: 400;
  line-height: 1.15;
  margin-bottom: 12px;
}
.section-sub {
  font-size: 14px;
  color: var(--muted);
  line-height: 1.75;
  max-width: 480px;
  margin-bottom: 48px;
}

/* ── LAYOUT ── */
.inner {
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 5vw;
}
section { padding: 88px 5vw; }

/* ── NAV ── */
.nav {
  position: fixed; top: 0; left: 0; right: 0; z-index: 200;
  height: 72px;
  background: var(--white);
  border-bottom: 1px solid #eee;
  display: flex; align-items: center; justify-content: space-between;
  padding: 0 5vw;
}
.nav-logo {
  display: flex; flex-direction: column; line-height: 1;
}
.nav-logo-name {
  font-family: 'Playfair Display', serif;
  font-size: 17px; font-weight: 400; color: var(--charcoal); letter-spacing: 0.03em;
}
.nav-logo-sub {
  font-size: 8px; font-weight: 600; letter-spacing: 0.28em;
  text-transform: uppercase; color: var(--taupe); margin-top: 3px;
}
.nav-links {
  display: flex; gap: 36px; list-style: none;
}
.nav-links a {
  font-size: 13px; font-weight: 400; color: #444;
  transition: color 150ms;
}
.nav-links a:hover { color: var(--charcoal); }
.nav-cta {
  background: var(--taupe); color: var(--white);
  padding: 10px 22px; border-radius: 9999px;
  font-size: 12px; font-weight: 600; letter-spacing: 0.06em;
  transition: opacity 200ms;
}
.nav-cta:hover { opacity: 0.85; }

/* ── FOOTER ── */
.footer {
  background: var(--charcoal);
  padding: 56px 5vw 32px;
}
.footer-inner {
  max-width: 1100px; margin: 0 auto;
  display: grid; grid-template-columns: 2fr 1fr 1fr 1fr; gap: 40px;
  margin-bottom: 40px;
}
.footer-name {
  font-family: 'Playfair Display', serif;
  font-size: 17px; color: var(--white); margin-bottom: 6px;
}
.footer-tagline {
  font-size: 12px; color: rgba(255,255,255,0.35); font-style: italic; line-height: 1.6;
}
.footer-col-title {
  font-size: 10px; font-weight: 600; letter-spacing: 0.2em;
  text-transform: uppercase; color: rgba(255,255,255,0.4); margin-bottom: 14px;
}
.footer-col a {
  display: block; font-size: 13px; color: rgba(255,255,255,0.55);
  margin-bottom: 8px; transition: color 150ms;
}
.footer-col a:hover { color: var(--white); }
.footer-copy {
  max-width: 1100px; margin: 0 auto;
  padding-top: 24px; border-top: 1px solid rgba(255,255,255,0.07);
  font-size: 11px; color: rgba(255,255,255,0.2);
}

/* ── PAGE BANNER (inner pages) ── */
.page-banner {
  position: relative; height: 50vh; min-height: 380px;
  margin-top: 72px;
  display: flex; align-items: center; justify-content: center;
  overflow: hidden; text-align: center;
}
.page-banner-bg {
  position: absolute; inset: 0;
  background-size: cover; background-position: center;
}
.page-banner-bg::after {
  content: '';
  position: absolute; inset: 0;
  background: rgba(0,0,0,0.45);
}
.page-banner-text { position: relative; z-index: 1; }
.page-banner-text .eyebrow { color: rgba(255,255,255,0.6); }
.page-banner-text .section-title { color: var(--white); margin-bottom: 0; }

/* ── SERVICE CARDS ── */
.cards-grid {
  display: grid; grid-template-columns: repeat(3, 1fr); gap: 32px;
}
.card-img {
  width: 100%; height: 300px; object-fit: cover;
}
.card-img-wrap { position: relative; }
.lang-badge {
  position: absolute; bottom: 12px; left: 12px;
  background: rgba(255,255,255,0.92);
  border-radius: 9999px;
  font-size: 10px; font-weight: 600; letter-spacing: 0.06em;
  color: var(--taupe); padding: 4px 12px;
}
.card-body { padding: 20px 0; }
.card-label {
  font-size: 10px; font-weight: 600; letter-spacing: 0.22em;
  text-transform: uppercase; color: var(--taupe); margin-bottom: 6px;
}
.card-title {
  font-family: 'Playfair Display', serif;
  font-size: 22px; font-weight: 400; color: var(--charcoal); margin-bottom: 8px;
}
.card-desc { font-size: 13px; color: var(--muted); line-height: 1.8; margin-bottom: 14px; }
.card-link {
  font-size: 11px; font-weight: 600; letter-spacing: 0.1em;
  text-transform: uppercase; color: var(--taupe);
  transition: opacity 150ms;
}
.card-link:hover { opacity: 0.7; }

/* ── BUTTONS ── */
.btn-primary {
  display: inline-block; background: var(--taupe); color: var(--white);
  padding: 13px 28px; border-radius: 9999px;
  font-size: 12px; font-weight: 600; letter-spacing: 0.06em;
  transition: opacity 200ms;
}
.btn-primary:hover { opacity: 0.85; }
.btn-outline {
  display: inline-block; border: 1.5px solid var(--taupe); color: var(--taupe);
  background: transparent;
  padding: 12px 26px; border-radius: 9999px;
  font-size: 12px; font-weight: 600; letter-spacing: 0.06em;
  transition: all 200ms;
}
.btn-outline:hover { background: var(--taupe); color: var(--white); }

/* ── TESTIMONIALS ── */
.testimonials { background: var(--cream); }
.testimonials-header { text-align: center; margin-bottom: 48px; }
.testimonials-header .section-sub { margin: 0 auto; text-align: center; }
.carousel { position: relative; overflow: hidden; }
.carousel-track {
  display: flex; transition: transform 400ms ease;
}
.testi-card {
  min-width: 100%; padding: 0 48px;
  display: grid; grid-template-columns: 1fr 1fr; gap: 24px;
}
.testi-item {
  background: var(--white); border-radius: 8px; padding: 32px;
}
.testi-stars { color: var(--taupe); font-size: 14px; letter-spacing: 3px; margin-bottom: 14px; }
.testi-quote {
  font-size: 14px; font-style: italic; color: #555;
  line-height: 1.85; margin-bottom: 20px;
}
.testi-name { font-size: 13px; font-weight: 600; color: var(--charcoal); }
.testi-sub { font-size: 11px; color: var(--muted); margin-top: 2px; }
.carousel-dots {
  display: flex; justify-content: center; gap: 8px; margin-top: 32px;
}
.carousel-dot {
  width: 8px; height: 8px; border-radius: 50%;
  background: var(--border); border: none; cursor: pointer; padding: 0;
  transition: background 200ms;
}
.carousel-dot.active { background: var(--taupe); }

/* ── CTA STRIP ── */
.cta-strip { background: var(--taupe); text-align: center; padding: 80px 5vw; }
.cta-strip .section-title { color: var(--white); max-width: 560px; margin: 0 auto 10px; }
.cta-strip-sub {
  font-size: 14px; color: rgba(255,255,255,0.75); margin-bottom: 28px; line-height: 1.7;
}
.cta-form {
  display: flex; gap: 8px; max-width: 400px; margin: 0 auto;
}
.cta-input {
  flex: 1; padding: 12px 18px; border-radius: 9999px; border: none;
  font-size: 13px; font-family: inherit; outline: none;
}
.cta-submit {
  background: var(--white); color: var(--taupe);
  padding: 12px 22px; border-radius: 9999px; border: none;
  font-size: 12px; font-weight: 700; font-family: inherit;
  cursor: pointer; white-space: nowrap; transition: opacity 200ms;
}
.cta-submit:hover { opacity: 0.88; }

/* ── PRICING ── */
.pricing-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 24px; max-width: 720px; }
.price-card {
  border: 1.5px solid var(--border); border-radius: 10px; padding: 32px;
}
.price-card.featured { border-color: var(--taupe); background: #fdf9f5; }
.price-badge {
  font-size: 10px; font-weight: 600; letter-spacing: 0.18em; text-transform: uppercase;
  color: var(--taupe); margin-bottom: 8px; display: block;
}
.price-name {
  font-family: 'Playfair Display', serif;
  font-size: 22px; font-weight: 400; color: var(--charcoal); margin-bottom: 4px;
}
.price-amount {
  font-size: 30px; font-weight: 300; color: var(--charcoal); margin: 12px 0 4px;
}
.price-amount span { font-size: 13px; color: var(--muted); font-weight: 400; }
.price-desc { font-size: 13px; color: var(--muted); line-height: 1.65; margin-bottom: 16px; }
.price-features {
  list-style: none; font-size: 13px; color: #666; line-height: 2; margin-bottom: 24px;
}
.price-features li::before { content: '✓ '; color: var(--taupe); font-weight: 600; }

/* ── ABOUT SPLIT ── */
.about-split {
  display: grid; grid-template-columns: 1fr 1fr; min-height: 560px;
}
.about-photo { overflow: hidden; }
.about-photo img { width: 100%; height: 100%; object-fit: cover; object-position: top; }
.about-content {
  padding: 72px 64px;
  display: flex; flex-direction: column; justify-content: center;
}
.about-body { font-size: 14px; color: var(--muted); line-height: 1.9; margin-bottom: 14px; }
.about-tags { display: flex; flex-wrap: wrap; gap: 8px; margin: 20px 0 28px; }
.about-tag {
  font-size: 10px; font-weight: 500; letter-spacing: 0.06em; text-transform: uppercase;
  border: 1px solid var(--border); border-radius: 9999px;
  padding: 4px 13px; color: #7a6040;
}
.about-tag.hi { background: var(--taupe); color: var(--white); border-color: var(--taupe); }
.cert-row {
  display: flex; gap: 12px; align-items: flex-start;
  padding-top: 18px; border-top: 1px solid var(--border); margin-top: 4px;
}
.cert-icon { font-size: 16px; flex-shrink: 0; margin-top: 1px; }
.cert-title { font-size: 13px; font-weight: 500; color: var(--charcoal); margin-bottom: 2px; }
.cert-sub { font-size: 12px; color: var(--muted); }

/* ── HOME HERO ── */
.hero {
  position: relative; height: 100vh; min-height: 620px;
  margin-top: 72px;
  display: flex; align-items: center; justify-content: flex-end;
  overflow: hidden;
}
.hero-bg {
  position: absolute; inset: 0;
  background-size: cover; background-position: center 20%;
}
.hero-bg::after {
  content: '';
  position: absolute; inset: 0;
  background: linear-gradient(to left, rgba(0,0,0,0.65) 0%, rgba(0,0,0,0.25) 55%, transparent 100%);
}
.hero-text {
  position: relative; z-index: 1;
  text-align: right; padding: 0 72px; max-width: 580px;
}
.hero-h1 {
  font-family: 'Playfair Display', serif;
  font-size: clamp(44px, 6vw, 78px); font-weight: 400;
  color: var(--white); line-height: 1.1; margin-bottom: 18px;
}
.hero-tagline {
  font-size: 16px; font-style: italic; color: rgba(255,255,255,0.6);
  line-height: 1.75; margin-bottom: 32px;
}
.hero-btn {
  display: inline-block;
  border: 1.5px solid rgba(255,255,255,0.65); color: var(--white);
  padding: 14px 32px; border-radius: 9999px;
  font-size: 12px; font-weight: 500; letter-spacing: 0.12em; text-transform: uppercase;
  backdrop-filter: blur(8px); background: rgba(255,255,255,0.1);
  transition: background 200ms;
}
.hero-btn:hover { background: rgba(255,255,255,0.2); }

/* ── SECONDARY IMAGE STRIP ── */
.img-strip { height: 360px; overflow: hidden; }
.img-strip img { width: 100%; height: 100%; object-fit: cover; object-position: center 30%; }

/* ── RESPONSIVE ── */
@media (max-width: 768px) {
  .nav-links { display: none; }
  section { padding: 64px 5vw; }
  .cards-grid { grid-template-columns: 1fr; }
  .about-split { grid-template-columns: 1fr; }
  .about-content { padding: 48px 24px; }
  .footer-inner { grid-template-columns: 1fr 1fr; }
  .pricing-grid { grid-template-columns: 1fr; }
  .testi-card { grid-template-columns: 1fr; padding: 0 16px; }
  .cta-form { flex-direction: column; }
}
@media (prefers-reduced-motion: reduce) {
  .carousel-track { transition: none; }
  html { scroll-behavior: auto; }
}
```

- [ ] **Step 2: Verify tokens load correctly**

Create a temp file `test.html` at the project root:
```html
<!DOCTYPE html>
<html><head><link rel="stylesheet" href="style.css">
<style>body{padding:40px}</style></head>
<body>
<span class="eyebrow">Eyebrow test</span>
<h2 class="section-title">Heading Test</h2>
<p class="section-sub">Body copy in Inter light.</p>
<a href="#" class="btn-primary">Primary Button</a>
<a href="#" class="btn-outline" style="margin-left:12px">Outline Button</a>
</body></html>
```
Open in browser. Verify: Playfair Display loads for `.section-title`, Inter loads for body, taupe color appears on eyebrow, buttons have correct border-radius.

- [ ] **Step 3: Delete `test.html` and commit**

```bash
rm test.html
git add style.css
git commit -m "feat: add shared style.css with design tokens, nav, footer, components"
```

---

## Task 2: Create `carousel.js`

**Files:**
- Create: `carousel.js`

- [ ] **Step 1: Write `carousel.js`**

```js
(function () {
  const track = document.querySelector('.carousel-track');
  const dots = document.querySelectorAll('.carousel-dot');
  if (!track || !dots.length) return;

  let current = 0;
  const total = dots.length;

  function goTo(index) {
    current = index;
    track.style.transform = `translateX(-${current * 100}%)`;
    dots.forEach((d, i) => d.classList.toggle('active', i === current));
  }

  dots.forEach((dot, i) => dot.addEventListener('click', () => goTo(i)));
  goTo(0);

  setInterval(() => goTo((current + 1) % total), 5000);
})();
```

- [ ] **Step 2: Commit**

```bash
git add carousel.js
git commit -m "feat: add vanilla JS testimonials carousel"
```

---

## Task 3: Build `index.html` — Home page

**Files:**
- Replace: `index.html`

- [ ] **Step 1: Write `index.html`**

```html
<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Thạch Dừa Studio — Yoga & Movement, TP. Hồ Chí Minh</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<!-- NAV -->
<nav class="nav">
  <a href="index.html" class="nav-logo">
    <span class="nav-logo-name">Thạch Dừa Studio</span>
    <span class="nav-logo-sub">Movement &amp; Somatic</span>
  </a>
  <ul class="nav-links">
    <li><a href="programs.html">Dịch vụ</a></li>
    <li><a href="about.html">Giới thiệu</a></li>
    <li><a href="pricing.html">Bảng giá</a></li>
  </ul>
  <a href="mailto:thachdua29@gmail.com" class="nav-cta">Đặt lịch ngay</a>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="hero-bg" style="background-image:url('images/2aoboqwjpbpxuohyoxawbfhjyfrezbrump8bomac4.jpg');"></div>
  <div class="hero-text">
    <span class="eyebrow" style="color:rgba(255,255,255,0.6);">Yoga · Movement · Somatic — TP. Hồ Chí Minh</span>
    <h1 class="hero-h1">
      Welcome to<br>
      <em>Thạch Dừa</em><br>
      Studio
    </h1>
    <p class="hero-tagline">Bắt nguồn từ cơ thể.<br>Powered by movement.</p>
    <a href="programs.html" class="hero-btn">Explore Programs</a>
  </div>
</section>

<!-- PROGRAMS PREVIEW -->
<section style="background:var(--white);">
  <div class="inner">
    <span class="eyebrow">Explore our programs</span>
    <h2 class="section-title">Programs</h2>
    <p class="section-sub">Chọn hình thức phù hợp với cơ thể, mục tiêu và lịch trình của bạn.</p>
    <div class="cards-grid">

      <div>
        <div class="card-img-wrap">
          <img class="card-img" src="images/2aoboqwjpfn8reksp76ifyfwxgduxieminqu508o15.jpg" alt="Private 1:1 yoga session">
          <span class="lang-badge">🇻🇳 VI · 🇬🇧 EN</span>
        </div>
        <div class="card-body">
          <div class="card-label">Private</div>
          <div class="card-title">Private 1:1</div>
          <p class="card-desc">Lộ trình, cường độ và mục tiêu được thiết kế hoàn toàn riêng cho bạn. Phù hợp người mới bắt đầu hoặc đang phục hồi chấn thương.</p>
          <a href="programs.html" class="card-link">Learn More →</a>
        </div>
      </div>

      <div>
        <div class="card-img-wrap">
          <img class="card-img" src="images/2aoboqwjpcphf2q485jx04hoiq3ceyb1tag0qavc7.jpg" alt="Small group yoga class">
          <span class="lang-badge">🇻🇳 VI · 🇬🇧 EN</span>
        </div>
        <div class="card-body">
          <div class="card-label">Group</div>
          <div class="card-title">Small Group 1:6</div>
          <p class="card-desc">Tối đa 6 người — năng lượng nhóm kết hợp sự chú ý cá nhân. Không khí ấm áp, cùng nhau phát triển trên thảm tập.</p>
          <a href="programs.html" class="card-link">Learn More →</a>
        </div>
      </div>

      <div>
        <div class="card-img-wrap">
          <img class="card-img" src="images/2aoboqwjpf3xjsj5gzhisjfq6zc9faot9e6muyiq14.jpg" alt="Flexible location yoga" style="object-position:center 35%;">
          <span class="lang-badge">🇻🇳 VI · 🇬🇧 EN</span>
        </div>
        <div class="card-body">
          <div class="card-label">Flexible</div>
          <div class="card-title">Linh hoạt địa điểm</div>
          <p class="card-desc">Tại studio, tại nhà học viên hoặc ngoài trời. Không gian thoải mái nhất cho hành trình của bạn.</p>
          <a href="programs.html" class="card-link">Learn More →</a>
        </div>
      </div>

    </div>
  </div>
</section>

<!-- TESTIMONIALS -->
<section class="testimonials">
  <div class="inner">
    <div class="testimonials-header">
      <span class="eyebrow">What people are saying</span>
      <h2 class="section-title">What Our Students Say</h2>
      <p class="section-sub">Discover how Thảo's students have transformed their practice.</p>
    </div>
    <div class="carousel">
      <div class="carousel-track">

        <!-- Slide 1: reviews 1 + 2 -->
        <div class="testi-card">
          <div class="testi-item">
            <div class="testi-stars">★★★★★</div>
            <p class="testi-quote">"Mình tập với Thảo được 2 tháng rồi, lưng đau mỏi giảm hẳn. Cô ấy rất chú ý đến từng tư thế và giải thích rõ tại sao phải làm đúng — không chỉ làm theo."</p>
            <div class="testi-name">Nguyễn Minh Thư</div>
            <div class="testi-sub">Private 1:1 · TP.HCM</div>
          </div>
          <div class="testi-item">
            <div class="testi-stars">★★★★★</div>
            <p class="testi-quote">"I was nervous joining as an expat but Thao made me feel so welcome. Her English instruction is clear and her alignment cues are incredibly precise."</p>
            <div class="testi-name">Sarah L.</div>
            <div class="testi-sub">Small Group · Ho Chi Minh City</div>
          </div>
        </div>

        <!-- Slide 2: reviews 3 + 4 -->
        <div class="testi-card">
          <div class="testi-item">
            <div class="testi-stars">★★★★★</div>
            <p class="testi-quote">"Thảo dạy tại nhà mình nên không phải lo di chuyển. Buổi học rất cá nhân hóa, phù hợp với thời gian và mục tiêu của mình."</p>
            <div class="testi-name">Trần Khánh Linh</div>
            <div class="testi-sub">Linh hoạt địa điểm · TP.HCM</div>
          </div>
          <div class="testi-item">
            <div class="testi-stars">★★★★★</div>
            <p class="testi-quote">"Thao is an exceptional teacher. She explains each movement clearly in English and I've seen incredible progress in my flexibility and core strength."</p>
            <div class="testi-name">James M.</div>
            <div class="testi-sub">Private 1:1 · District 2</div>
          </div>
        </div>

        <!-- Slide 3: review 5 solo -->
        <div class="testi-card">
          <div class="testi-item">
            <div class="testi-stars">★★★★★</div>
            <p class="testi-quote">"Nhóm nhỏ 6 người rất ấm cúng. Thảo để ý đến từng người dù dạy nhóm — cảm giác như được học riêng vậy."</p>
            <div class="testi-name">Lê Phương Anh</div>
            <div class="testi-sub">Small Group · TP.HCM</div>
          </div>
          <div class="testi-item" style="visibility:hidden;"></div>
        </div>

      </div>
      <div class="carousel-dots">
        <button class="carousel-dot active" aria-label="Slide 1"></button>
        <button class="carousel-dot" aria-label="Slide 2"></button>
        <button class="carousel-dot" aria-label="Slide 3"></button>
      </div>
    </div>
  </div>
</section>

<!-- CTA STRIP -->
<section class="cta-strip">
  <h2 class="section-title">Ready to start your wellness journey?</h2>
  <p class="cta-strip-sub">Đặt buổi học thử miễn phí — không cam kết, không áp lực.<br>Thảo sẽ liên hệ trong vòng 24 giờ.</p>
  <form class="cta-form" onsubmit="window.location='mailto:thachdua29@gmail.com?subject=Đặt lịch học thử';return false;">
    <input class="cta-input" type="email" placeholder="Email của bạn…" required>
    <button class="cta-submit" type="submit">Start Today</button>
  </form>
</section>

<!-- FOOTER -->
<footer class="footer">
  <div class="footer-inner">
    <div>
      <div class="footer-name">Thạch Dừa Studio</div>
      <div class="footer-tagline">Bắt nguồn từ cơ thể.<br>Powered by movement.</div>
    </div>
    <div class="footer-col">
      <div class="footer-col-title">Studio</div>
      <a href="programs.html">Dịch vụ</a>
      <a href="about.html">Giới thiệu</a>
      <a href="pricing.html">Bảng giá</a>
    </div>
    <div class="footer-col">
      <div class="footer-col-title">Connect</div>
      <a href="https://www.instagram.com/thach_dua/" target="_blank" rel="noopener">Instagram</a>
      <a href="https://www.facebook.com/dua.thach.2906/" target="_blank" rel="noopener">Facebook</a>
      <a href="https://www.threads.com/@thach_dua" target="_blank" rel="noopener">Threads</a>
    </div>
    <div class="footer-col">
      <div class="footer-col-title">Contact Us</div>
      <a href="mailto:thachdua29@gmail.com">thachdua29@gmail.com</a>
      <a href="tel:0703786631">0703 786 631</a>
    </div>
  </div>
  <div class="footer-copy">© 2025 Thạch Dừa Studio · TP. Hồ Chí Minh</div>
</footer>

<script src="carousel.js"></script>
</body>
</html>
```

- [ ] **Step 2: Open `index.html` in browser and verify**

Check:
- Nav is white, fixed at top, logo renders in Playfair Display
- Hero is full-screen with photo, text right-aligned, readable white text
- 3 program cards show correct photos with VI·EN badge bottom-left
- Testimonial carousel shows 2 reviews per slide, dots auto-advance every 5s
- CTA strip is taupe background
- Footer is dark charcoal, 4-column

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: build home page — hero, programs preview, testimonials, CTA"
```

---

## Task 4: Build `programs.html`

**Files:**
- Create: `programs.html`

- [ ] **Step 1: Write `programs.html`**

```html
<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Programs — Thạch Dừa Studio</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<!-- NAV -->
<nav class="nav">
  <a href="index.html" class="nav-logo">
    <span class="nav-logo-name">Thạch Dừa Studio</span>
    <span class="nav-logo-sub">Movement &amp; Somatic</span>
  </a>
  <ul class="nav-links">
    <li><a href="programs.html">Dịch vụ</a></li>
    <li><a href="about.html">Giới thiệu</a></li>
    <li><a href="pricing.html">Bảng giá</a></li>
  </ul>
  <a href="mailto:thachdua29@gmail.com" class="nav-cta">Đặt lịch ngay</a>
</nav>

<!-- PAGE BANNER -->
<div class="page-banner">
  <div class="page-banner-bg" style="background-image:url('images/2aoboqwjpam0hdsjgttoadzrpmo6yn5l3ioddzjw1.jpg');"></div>
  <div class="page-banner-text">
    <span class="eyebrow">Explore our programs</span>
    <h1 class="section-title">Programs</h1>
  </div>
</div>

<!-- SERVICE CARDS -->
<section style="background:var(--white);">
  <div class="inner">
    <p class="section-sub" style="margin-bottom:48px;">
      Chọn hình thức phù hợp với cơ thể, mục tiêu và lịch trình của bạn.<br>
      Tất cả chương trình đều có thể giảng dạy bằng Tiếng Việt hoặc Tiếng Anh.
    </p>
    <div class="cards-grid">

      <div>
        <div class="card-img-wrap">
          <img class="card-img" src="images/2aoboqwjpfn8reksp76ifyfwxgduxieminqu508o15.jpg" alt="Private 1:1 yoga — warrior III balance pose">
          <span class="lang-badge">🇻🇳 VI · 🇬🇧 EN</span>
        </div>
        <div class="card-body">
          <div class="card-label">Private</div>
          <div class="card-title">Private 1:1</div>
          <p class="card-desc">Buổi học hoàn toàn cá nhân hóa — lộ trình, cường độ và mục tiêu được thiết kế riêng cho bạn. Phù hợp với người mới bắt đầu hoặc đang phục hồi chấn thương. Thảo sẽ lắng nghe cơ thể bạn trước khi hướng dẫn.</p>
          <a href="mailto:thachdua29@gmail.com?subject=Đặt lịch Private 1:1" class="btn-primary" style="font-size:11px;padding:10px 22px;">Đặt lịch →</a>
        </div>
      </div>

      <div>
        <div class="card-img-wrap">
          <img class="card-img" src="images/2aoboqwjpcphf2q485jx04hoiq3ceyb1tag0qavc7.jpg" alt="Small group yoga class — side-lying extension">
          <span class="lang-badge">🇻🇳 VI · 🇬🇧 EN</span>
        </div>
        <div class="card-body">
          <div class="card-label">Group</div>
          <div class="card-title">Small Group 1:6</div>
          <p class="card-desc">Lớp nhỏ tối đa 6 người — năng lượng nhóm kết hợp sự chú ý cá nhân. Không khí ấm áp, cùng nhau phát triển trên thảm tập. Thảo vẫn đảm bảo căn chỉnh tư thế cho từng người.</p>
          <a href="mailto:thachdua29@gmail.com?subject=Đặt lịch Small Group" class="btn-primary" style="font-size:11px;padding:10px 22px;">Đặt lịch →</a>
        </div>
      </div>

      <div>
        <div class="card-img-wrap">
          <img class="card-img" src="images/2aoboqwjpf3xjsj5gzhisjfq6zc9faot9e6muyiq14.jpg" alt="Flexible location yoga — sphinx pose" style="object-position:center 35%;">
          <span class="lang-badge">🇻🇳 VI · 🇬🇧 EN</span>
        </div>
        <div class="card-body">
          <div class="card-label">Flexible</div>
          <div class="card-title">Linh hoạt địa điểm</div>
          <p class="card-desc">Tại studio, tại nhà học viên hoặc ngoài trời. Thảo mang thảm và thiết bị đến tận nơi bạn chọn. Trải nghiệm tập luyện thoải mái nhất trong không gian quen thuộc của bạn.</p>
          <a href="mailto:thachdua29@gmail.com?subject=Đặt lịch Flexible" class="btn-primary" style="font-size:11px;padding:10px 22px;">Đặt lịch →</a>
        </div>
      </div>

    </div>
  </div>
</section>

<!-- CTA STRIP -->
<section class="cta-strip">
  <h2 class="section-title">Not sure which program is right for you?</h2>
  <p class="cta-strip-sub">Nhắn tin cho Thảo — buổi tư vấn 15 phút miễn phí để tìm ra hình thức phù hợp nhất.</p>
  <a href="mailto:thachdua29@gmail.com" class="btn-primary" style="background:var(--white);color:var(--taupe);">Liên hệ Thảo →</a>
</section>

<!-- FOOTER -->
<footer class="footer">
  <div class="footer-inner">
    <div>
      <div class="footer-name">Thạch Dừa Studio</div>
      <div class="footer-tagline">Bắt nguồn từ cơ thể.<br>Powered by movement.</div>
    </div>
    <div class="footer-col">
      <div class="footer-col-title">Studio</div>
      <a href="programs.html">Dịch vụ</a>
      <a href="about.html">Giới thiệu</a>
      <a href="pricing.html">Bảng giá</a>
    </div>
    <div class="footer-col">
      <div class="footer-col-title">Connect</div>
      <a href="https://www.instagram.com/thach_dua/" target="_blank" rel="noopener">Instagram</a>
      <a href="https://www.facebook.com/dua.thach.2906/" target="_blank" rel="noopener">Facebook</a>
      <a href="https://www.threads.com/@thach_dua" target="_blank" rel="noopener">Threads</a>
    </div>
    <div class="footer-col">
      <div class="footer-col-title">Contact Us</div>
      <a href="mailto:thachdua29@gmail.com">thachdua29@gmail.com</a>
      <a href="tel:0703786631">0703 786 631</a>
    </div>
  </div>
  <div class="footer-copy">© 2025 Thạch Dừa Studio · TP. Hồ Chí Minh</div>
</footer>

</body>
</html>
```

- [ ] **Step 2: Open `programs.html` in browser and verify**

Check:
- Banner image fills top 50vh with dark overlay and centered text
- 3 cards show correct photos, VI·EN badge, longer descriptions, "Đặt lịch →" button
- Taupe CTA strip at bottom with white button
- Nav and footer match `index.html` exactly

- [ ] **Step 3: Commit**

```bash
git add programs.html
git commit -m "feat: build programs page — banner and 3 service cards"
```

---

## Task 5: Build `about.html`

**Files:**
- Create: `about.html`

- [ ] **Step 1: Write `about.html`**

```html
<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>About — Thạch Dừa Studio</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<!-- NAV -->
<nav class="nav">
  <a href="index.html" class="nav-logo">
    <span class="nav-logo-name">Thạch Dừa Studio</span>
    <span class="nav-logo-sub">Movement &amp; Somatic</span>
  </a>
  <ul class="nav-links">
    <li><a href="programs.html">Dịch vụ</a></li>
    <li><a href="about.html">Giới thiệu</a></li>
    <li><a href="pricing.html">Bảng giá</a></li>
  </ul>
  <a href="mailto:thachdua29@gmail.com" class="nav-cta">Đặt lịch ngay</a>
</nav>

<!-- PAGE BANNER -->
<div class="page-banner">
  <div class="page-banner-bg" style="background-image:url('images/2aoboqwjpelzb93t9tnogm1sgfkuivyl9txvhwbi13.jpg');background-position:center top;"></div>
  <div class="page-banner-text">
    <span class="eyebrow">About</span>
    <h1 class="section-title">Meet Thạch Thảo</h1>
  </div>
</div>

<!-- SPLIT BIO -->
<div class="about-split">
  <div class="about-photo">
    <img src="images/2aoboqwjpelzb93t9tnogm1sgfkuivyl9txvhwbi13.jpg" alt="Thạch Thảo — yoga instructor">
  </div>
  <div class="about-content">
    <span class="eyebrow">About</span>
    <h2 class="section-title" style="margin-bottom:20px;">Meet Thạch Thảo</h2>
    <p class="about-body">Thạch Thảo là Yoga &amp; Movement Instructor với chuyên môn sâu về somatic movement và giải phẫu học ứng dụng. Cách tiếp cận tập luyện đặt alignment, breath control và kết nối cơ thể–tâm trí lên hàng đầu.</p>
    <p class="about-body">Giảng dạy bằng cả <strong>Tiếng Việt và Tiếng Anh</strong> — thân thiện với học viên trong nước lẫn expat tại TP.HCM. Mỗi buổi học được thiết kế riêng cho từng người.</p>
    <p class="about-body">Với nền tảng Marketing và niềm đam mê chuyển động, Thảo mang đến những buổi học không chỉ hiệu quả về thể chất mà còn là trải nghiệm đáng nhớ — ấm áp, cá nhân và truyền cảm hứng.</p>
    <div class="about-tags">
      <span class="about-tag hi">🇻🇳 Tiếng Việt</span>
      <span class="about-tag hi">🇬🇧 English</span>
      <span class="about-tag">Alignment</span>
      <span class="about-tag">Somatic</span>
      <span class="about-tag">Breath Work</span>
      <span class="about-tag">200h YTT</span>
      <span class="about-tag">Injury Prevention</span>
    </div>
    <div class="cert-row">
      <div class="cert-icon">⭐</div>
      <div>
        <div class="cert-title">200-Hour Yoga Teacher Training Certificate</div>
        <div class="cert-sub">Yoga Alliance · Chứng nhận quốc tế · 2024</div>
      </div>
    </div>
    <div class="cert-row">
      <div class="cert-icon">🎓</div>
      <div>
        <div class="cert-title">Cử nhân Marketing</div>
        <div class="cert-sub">Đại học Tôn Đức Thắng · 2024</div>
      </div>
    </div>
  </div>
</div>

<!-- SECONDARY IMAGE STRIP -->
<div class="img-strip">
  <img src="images/2aoboqwjpb0izstdcjy0wo6v5sdwgmvvrkfdzyre3.jpg" alt="Thạch Thảo — forward fold practice">
</div>

<!-- CTA STRIP -->
<section class="cta-strip">
  <h2 class="section-title">Ready to practice together?</h2>
  <p class="cta-strip-sub">Đặt buổi học thử miễn phí và cùng Thảo khám phá hành trình chuyển động của bạn.</p>
  <a href="mailto:thachdua29@gmail.com" class="btn-primary" style="background:var(--white);color:var(--taupe);">Đặt lịch ngay →</a>
</section>

<!-- FOOTER -->
<footer class="footer">
  <div class="footer-inner">
    <div>
      <div class="footer-name">Thạch Dừa Studio</div>
      <div class="footer-tagline">Bắt nguồn từ cơ thể.<br>Powered by movement.</div>
    </div>
    <div class="footer-col">
      <div class="footer-col-title">Studio</div>
      <a href="programs.html">Dịch vụ</a>
      <a href="about.html">Giới thiệu</a>
      <a href="pricing.html">Bảng giá</a>
    </div>
    <div class="footer-col">
      <div class="footer-col-title">Connect</div>
      <a href="https://www.instagram.com/thach_dua/" target="_blank" rel="noopener">Instagram</a>
      <a href="https://www.facebook.com/dua.thach.2906/" target="_blank" rel="noopener">Facebook</a>
      <a href="https://www.threads.com/@thach_dua" target="_blank" rel="noopener">Threads</a>
    </div>
    <div class="footer-col">
      <div class="footer-col-title">Contact Us</div>
      <a href="mailto:thachdua29@gmail.com">thachdua29@gmail.com</a>
      <a href="tel:0703786631">0703 786 631</a>
    </div>
  </div>
  <div class="footer-copy">© 2025 Thạch Dừa Studio · TP. Hồ Chí Minh</div>
</footer>

</body>
</html>
```

- [ ] **Step 2: Open `about.html` in browser and verify**

Check:
- Banner shows back-view photo with centered "Meet Thạch Thảo" heading
- Split bio: photo fills full left column height, right column has bio + tags + certs
- VI·EN tags appear highlighted in taupe, other tags are outlined
- Secondary image strip is full-width, 360px tall
- CTA strip and footer match other pages

- [ ] **Step 3: Commit**

```bash
git add about.html
git commit -m "feat: build about page — bio, credentials, secondary image"
```

---

## Task 6: Build `pricing.html`

**Files:**
- Create: `pricing.html`

- [ ] **Step 1: Write `pricing.html`**

```html
<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Pricing — Thạch Dừa Studio</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<!-- NAV -->
<nav class="nav">
  <a href="index.html" class="nav-logo">
    <span class="nav-logo-name">Thạch Dừa Studio</span>
    <span class="nav-logo-sub">Movement &amp; Somatic</span>
  </a>
  <ul class="nav-links">
    <li><a href="programs.html">Dịch vụ</a></li>
    <li><a href="about.html">Giới thiệu</a></li>
    <li><a href="pricing.html">Bảng giá</a></li>
  </ul>
  <a href="mailto:thachdua29@gmail.com" class="nav-cta">Đặt lịch ngay</a>
</nav>

<!-- PAGE BANNER -->
<div class="page-banner">
  <div class="page-banner-bg" style="background-image:url('images/2aoboqwjpdge0szcgu1l2tpakqy9vz5xwgc1wczw9.jpg');background-position:center 30%;"></div>
  <div class="page-banner-text">
    <span class="eyebrow">Pricing</span>
    <h1 class="section-title">Choose Your Plan</h1>
  </div>
</div>

<!-- PRICING CARDS -->
<section style="background:var(--white);">
  <div class="inner">
    <p class="section-sub">Linh hoạt theo mục tiêu — đặt lịch bất cứ lúc nào. Tất cả buổi học đều có thể giảng dạy bằng Tiếng Việt hoặc Tiếng Anh.</p>
    <div class="pricing-grid">

      <div class="price-card">
        <span class="price-badge">Single Session</span>
        <div class="price-name">Buổi lẻ</div>
        <div class="price-amount">350.000 <span>VND / buổi</span></div>
        <p class="price-desc">Thử một buổi không cam kết — phù hợp nếu bạn muốn trải nghiệm trước khi đăng ký gói.</p>
        <ul class="price-features">
          <li>1 buổi tập 60 phút</li>
          <li>Private 1:1 hoặc Small Group</li>
          <li>Tiếng Việt hoặc Tiếng Anh</li>
          <li>Linh hoạt địa điểm</li>
        </ul>
        <a href="mailto:thachdua29@gmail.com?subject=Đặt lịch buổi lẻ" class="btn-outline">Đặt lịch</a>
      </div>

      <div class="price-card featured">
        <span class="price-badge">✦ Best Value</span>
        <div class="price-name">Gói 10 buổi</div>
        <div class="price-amount">2.800.000 <span>VND / gói</span></div>
        <p class="price-desc">Cam kết hành trình — tiết kiệm hơn &amp; được ưu tiên đặt lịch. Hiệu lực 3 tháng.</p>
        <ul class="price-features">
          <li>10 buổi tập 60 phút</li>
          <li>Linh hoạt hình thức &amp; địa điểm</li>
          <li>Tiếng Việt hoặc Tiếng Anh</li>
          <li>Hiệu lực 3 tháng</li>
          <li>Ưu tiên đặt lịch</li>
        </ul>
        <a href="mailto:thachdua29@gmail.com?subject=Đặt gói 10 buổi" class="btn-primary">Đặt lịch</a>
      </div>

    </div>

    <!-- CONTACT PROMPT -->
    <div style="margin-top:56px;padding-top:40px;border-top:1px solid var(--border);text-align:center;">
      <p style="font-size:14px;color:var(--muted);line-height:1.8;">
        Có câu hỏi về pricing? · Have questions about pricing?<br>
        <a href="mailto:thachdua29@gmail.com" style="color:var(--taupe);font-weight:500;">thachdua29@gmail.com</a>
        &nbsp;·&nbsp;
        <a href="tel:0703786631" style="color:var(--taupe);font-weight:500;">0703 786 631</a>
      </p>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer class="footer">
  <div class="footer-inner">
    <div>
      <div class="footer-name">Thạch Dừa Studio</div>
      <div class="footer-tagline">Bắt nguồn từ cơ thể.<br>Powered by movement.</div>
    </div>
    <div class="footer-col">
      <div class="footer-col-title">Studio</div>
      <a href="programs.html">Dịch vụ</a>
      <a href="about.html">Giới thiệu</a>
      <a href="pricing.html">Bảng giá</a>
    </div>
    <div class="footer-col">
      <div class="footer-col-title">Connect</div>
      <a href="https://www.instagram.com/thach_dua/" target="_blank" rel="noopener">Instagram</a>
      <a href="https://www.facebook.com/dua.thach.2906/" target="_blank" rel="noopener">Facebook</a>
      <a href="https://www.threads.com/@thach_dua" target="_blank" rel="noopener">Threads</a>
    </div>
    <div class="footer-col">
      <div class="footer-col-title">Contact Us</div>
      <a href="mailto:thachdua29@gmail.com">thachdua29@gmail.com</a>
      <a href="tel:0703786631">0703 786 631</a>
    </div>
  </div>
  <div class="footer-copy">© 2025 Thạch Dừa Studio · TP. Hồ Chí Minh</div>
</footer>

</body>
</html>
```

- [ ] **Step 2: Open `pricing.html` in browser and verify**

Check:
- Banner shows lying leg-raise photo, centered "Choose Your Plan"
- 2 price cards side by side — featured card has taupe border + cream background
- Checkmark feature list renders with taupe ✓ prefix
- "Buổi lẻ" has outline button, "Gói 10 buổi" has filled taupe button
- Contact prompt line appears below cards with taupe email/phone links

- [ ] **Step 3: Commit**

```bash
git add pricing.html
git commit -m "feat: build pricing page — two session packages"
```

---

## Task 7: Cross-page review and final commit

**Files:** All HTML files, `style.css`

- [ ] **Step 1: Check nav active state**

Add `style="color:var(--charcoal);font-weight:500;"` inline to the current page's nav link on each page so the active link is visually distinct. For example, on `programs.html` the "Dịch vụ" link gets the inline style.

- [ ] **Step 2: Verify mobile at 768px**

Open each page in browser DevTools at 768px width. Verify:
- Nav links hidden (only logo + CTA button visible)
- Hero text is centered and readable
- Cards stack to single column
- About split stacks (photo top, content below)
- Pricing cards stack to single column
- Footer stacks to 2-column grid

- [ ] **Step 3: Add `.gitignore` entry for brainstorm artifacts**

```bash
echo ".superpowers/" >> .gitignore
git add .gitignore
```

- [ ] **Step 4: Final commit**

```bash
git add index.html programs.html about.html pricing.html style.css carousel.js .gitignore
git commit -m "feat: complete Thạch Dừa Studio — CWS-style 4-page site"
```
