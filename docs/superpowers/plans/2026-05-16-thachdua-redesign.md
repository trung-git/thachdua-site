# Thạch Thảo Site Redesign — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace `index.html` with a Courtney Watts-style redesign using real photos, Poppins font, black/cream/brown palette, and a full-bleed hero + photo-card services + dark split about layout.

**Architecture:** Single self-contained `index.html` file — all CSS inline in `<style>`, no JS, no build step. Images referenced as `images/<filename>.jpg` relative to project root. The approved mockup at `mockup-preview.html` is the reference; this plan rebuilds it as the final `index.html`.

**Tech Stack:** HTML5, CSS3 (custom properties, grid, clamp), Google Fonts (Poppins)

---

## File Map

| File | Action | Purpose |
|---|---|---|
| `index.html` | **Rewrite** | Final production page |
| `mockup-preview.html` | **Delete** | Temp brainstorm file, superseded by index.html |
| `.gitignore` | **Update** | Add `.superpowers/` |

---

### Task 1: Base structure, CSS tokens, and Nav

**Files:**
- Modify: `index.html` (full rewrite)

- [ ] **Step 1: Replace index.html with the HTML skeleton + all CSS tokens + nav**

Overwrite `index.html` with the following complete file. This sets up the design token variables, global reset, Poppins font, and the fixed nav:

```html
<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Nguyễn Thạch Thảo — Movement & Somatic Instructor</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,300;0,400;0,500;0,600;0,700;1,300;1,400&display=swap" rel="stylesheet">
<style>
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

:root {
  --black: #000000;
  --cream: #f8f6f2;
  --brown: #8a7b67;
  --text: #1f2937;
  --muted: #4b5563;
  --faint: #6b7280;
  --border: #e5e7eb;
  --border-m: #d1d5db;
  --white: #ffffff;
}

html { scroll-behavior: smooth; }

body {
  font-family: 'Poppins', ui-sans-serif, system-ui, sans-serif;
  font-weight: 300;
  font-size: 16px;
  line-height: 24px;
  background: var(--white);
  color: var(--text);
  overflow-x: hidden;
}

/* ── NAV ── */
nav {
  position: fixed; top: 0; left: 0; right: 0; z-index: 200;
  display: flex; justify-content: space-between; align-items: center;
  padding: 0 5vw; height: 64px;
  background: rgba(0,0,0,0.72);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
}
.nav-logo {
  font-size: 16px; font-weight: 600; letter-spacing: 0.08em;
  color: var(--white); text-decoration: none; text-transform: uppercase;
}
.nav-links { display: flex; gap: 32px; list-style: none; align-items: center; }
.nav-links a {
  font-size: 12px; font-weight: 400; letter-spacing: 0.1em;
  text-transform: uppercase; color: rgba(255,255,255,0.7);
  text-decoration: none; transition: color 150ms;
}
.nav-links a:hover, .nav-links a:focus-visible { color: var(--white); }
.nav-links a:focus-visible { outline: 2px solid var(--white); outline-offset: 4px; border-radius: 2px; }
.nav-cta {
  background: var(--white); color: var(--black);
  padding: 8px 20px; border-radius: 9999px;
  font-size: 12px; font-weight: 600; letter-spacing: 0.06em; text-transform: uppercase;
  text-decoration: none; transition: opacity 200ms;
}
.nav-cta:hover { opacity: 0.85; }
.nav-cta:focus-visible { outline: 2px solid var(--white); outline-offset: 4px; }

/* ── SECTION COMMONS ── */
section { padding: 96px 5vw; scroll-margin-top: 64px; }
.inner { max-width: 1100px; margin: 0 auto; }
.s-eye {
  font-size: 11px; font-weight: 600; letter-spacing: 0.25em;
  text-transform: uppercase; color: var(--brown); margin-bottom: 12px;
}
.s-head {
  font-size: clamp(28px, 4vw, 46px); font-weight: 300;
  color: var(--text); line-height: 1.1; margin-bottom: 16px; letter-spacing: -0.01em;
}
.s-head strong { font-weight: 700; }
.s-head-light { color: var(--white); }
.s-sub {
  font-size: 15px; color: var(--faint);
  max-width: 520px; line-height: 1.75; margin-bottom: 48px;
}

/* ── RESPONSIVE NAV ── */
@media (max-width: 768px) {
  .nav-links { display: none; }
}
</style>
</head>
<body>

<nav>
  <a href="#" class="nav-logo">Thạch Thảo</a>
  <ul class="nav-links">
    <li><a href="#services">Dịch vụ</a></li>
    <li><a href="#about">Giới thiệu</a></li>
    <li><a href="#journey">Hành trình</a></li>
    <li><a href="#contact" class="nav-cta">Liên hệ</a></li>
  </ul>
</nav>

</body>
</html>
```

- [ ] **Step 2: Verify in browser**

Open `http://localhost:8890/index.html`. Check:
- Fixed dark nav visible at top
- "Thạch Thảo" logo in white uppercase
- Nav links visible on desktop, hidden on mobile
- "Liên hệ" button is a white pill

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: base structure, design tokens, nav"
```

---

### Task 2: Hero section

**Files:**
- Modify: `index.html` — add hero CSS inside `<style>` and hero HTML inside `<body>` after `</nav>`

- [ ] **Step 1: Add hero CSS**

Inside the `<style>` block, before the `@media` query, add:

```css
/* ── HERO ── */
.hero {
  position: relative; width: 100%; height: 100vh; min-height: 640px;
  display: flex; flex-direction: column; align-items: center; justify-content: center;
  text-align: center; overflow: hidden;
}
.hero-bg {
  position: absolute; inset: 0;
  background-image: url('images/2aoboqwjpbpxuohyoxawbfhjyfrezbrump8bomac4.jpg');
  background-size: cover; background-position: center 20%;
}
.hero-bg::after {
  content: '';
  position: absolute; inset: 0;
  background: linear-gradient(to bottom, rgba(0,0,0,0.4) 0%, rgba(0,0,0,0.62) 60%, rgba(0,0,0,0.82) 100%);
}
.hero-content {
  position: relative; z-index: 1; padding: 0 24px; max-width: 740px;
}
.hero-eyebrow {
  font-size: 11px; font-weight: 500; letter-spacing: 0.25em;
  text-transform: uppercase; color: var(--brown); margin-bottom: 20px; display: block;
}
.hero-h1 {
  font-size: clamp(44px, 7vw, 82px); font-weight: 300;
  color: var(--white); line-height: 1.0; margin-bottom: 18px; letter-spacing: -0.025em;
}
.hero-h1 strong { font-weight: 700; display: block; }
.hero-tagline {
  font-size: clamp(14px, 1.6vw, 17px); font-weight: 300; font-style: italic;
  color: rgba(255,255,255,0.65); margin-bottom: 36px; line-height: 1.65;
}
.hero-btn {
  display: inline-block; background: var(--white); color: var(--black);
  padding: 14px 34px; border-radius: 9999px;
  font-size: 13px; font-weight: 700; letter-spacing: 0.08em; text-transform: uppercase;
  text-decoration: none; transition: opacity 200ms;
}
.hero-btn:hover { opacity: 0.88; }
.hero-btn:focus-visible { outline: 2px solid var(--white); outline-offset: 4px; }
.hero-statsbar {
  position: absolute; bottom: 0; left: 0; right: 0; z-index: 1;
  display: grid; grid-template-columns: repeat(3, 1fr);
  background: rgba(0,0,0,0.55); backdrop-filter: blur(12px);
  border-top: 1px solid rgba(255,255,255,0.1);
}
.hero-stat {
  padding: 22px 0; text-align: center;
  border-right: 1px solid rgba(255,255,255,0.1);
}
.hero-stat:last-child { border-right: none; }
.hero-stat-val {
  font-size: 26px; font-weight: 300; color: var(--white); line-height: 1; margin-bottom: 5px;
}
.hero-stat-lbl {
  font-size: 10px; font-weight: 500; letter-spacing: 0.15em;
  text-transform: uppercase; color: rgba(255,255,255,0.38);
}

@media (max-width: 768px) {
  .hero { min-height: 100svh; }
}
```

- [ ] **Step 2: Add hero HTML**

After `</nav>` in `<body>`, add:

```html
<!-- HERO -->
<section class="hero">
  <div class="hero-bg"></div>
  <div class="hero-content">
    <span class="hero-eyebrow">Yoga · Movement · Somatic — TP. Hồ Chí Minh</span>
    <h1 class="hero-h1">
      Nguyễn
      <strong>Thạch Thảo</strong>
    </h1>
    <p class="hero-tagline">Bắt nguồn từ cơ thể.<br>Chuyển hóa qua chuyển động.</p>
    <a href="#services" class="hero-btn">Xem dịch vụ</a>
  </div>
  <div class="hero-statsbar">
    <div class="hero-stat">
      <div class="hero-stat-val">200h</div>
      <div class="hero-stat-lbl">YTT Cert</div>
    </div>
    <div class="hero-stat">
      <div class="hero-stat-val">70%</div>
      <div class="hero-stat-lbl">Tái đăng ký</div>
    </div>
    <div class="hero-stat">
      <div class="hero-stat-val">–30%</div>
      <div class="hero-stat-lbl">Đau mỏi sau 10 buổi</div>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Verify in browser**

Open `http://localhost:8890/index.html`. Check:
- Full-viewport dark hero with the balance-pose photo visible through overlay
- "Nguyễn" in light weight, "Thạch Thảo" in bold below it
- Brown eyebrow text, italic tagline, white pill CTA button
- Stats bar pinned to bottom with 3 columns and dividers
- On mobile: hero fills 100svh

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: hero section with full-bleed photo and stats bar"
```

---

### Task 3: Services section

**Files:**
- Modify: `index.html` — add services CSS and HTML

- [ ] **Step 1: Add services CSS**

Add inside `<style>`, before the final `@media` block:

```css
/* ── SERVICES ── */
.services { background: var(--cream); }
.services-header { text-align: center; }
.services-header .s-eye,
.services-header .s-head,
.services-header .s-sub { margin-left: auto; margin-right: auto; text-align: center; }
.services-grid {
  display: grid; grid-template-columns: repeat(2, 1fr);
  gap: 20px; margin-top: 48px;
}
.svc-card {
  background: var(--white); border: 1px solid var(--border);
  border-radius: 12px; overflow: hidden;
  transition: box-shadow 200ms, transform 200ms;
}
.svc-card:hover {
  box-shadow: 0 10px 15px -3px rgba(0,0,0,.08), 0 4px 6px -4px rgba(0,0,0,.08);
  transform: translateY(-3px);
}
.svc-img { width: 100%; height: 240px; object-fit: cover; display: block; }
.svc-body { padding: 24px 26px; }
.svc-num {
  font-size: 10px; font-weight: 600; letter-spacing: 0.2em;
  color: var(--brown); text-transform: uppercase; margin-bottom: 8px;
}
.svc-title { font-size: 19px; font-weight: 600; color: var(--text); margin-bottom: 10px; }
.svc-desc { font-size: 13px; color: var(--muted); line-height: 1.8; margin-bottom: 18px; }
.svc-cta {
  font-size: 12px; font-weight: 600; letter-spacing: 0.1em;
  text-transform: uppercase; color: var(--brown); text-decoration: none;
}
.svc-cta::after { content: ' →'; }
.svc-cta:focus-visible { outline: 2px solid var(--brown); outline-offset: 4px; border-radius: 2px; }

@media (max-width: 768px) {
  .services-grid { grid-template-columns: 1fr; }
}
```

- [ ] **Step 2: Add services HTML**

After the hero `</section>`, add:

```html
<!-- SERVICES -->
<section class="services" id="services">
  <div class="inner">
    <div class="services-header">
      <p class="s-eye">Dịch vụ</p>
      <h2 class="s-head">Chọn hình thức <strong>tập luyện</strong></h2>
      <p class="s-sub">Mỗi buổi học được thiết kế riêng để phù hợp với cơ thể, mục tiêu và lịch trình của bạn.</p>
    </div>
    <div class="services-grid">
      <div class="svc-card">
        <img class="svc-img" src="images/2aoboqwjpc2wkuicbemjozt0qli3bupcn0mto7o86.jpg"
             alt="Tư thế yoga cá nhân — kneeling arm raise"
             style="object-position: center 30%;">
        <div class="svc-body">
          <div class="svc-num">01 · Private</div>
          <div class="svc-title">Private 1:1</div>
          <p class="svc-desc">Buổi học hoàn toàn cá nhân hóa — lộ trình, cường độ và mục tiêu được thiết kế riêng cho bạn. Phù hợp với người mới bắt đầu hoặc phục hồi chấn thương.</p>
          <a href="#contact" class="svc-cta">Đăng ký</a>
        </div>
      </div>
      <div class="svc-card">
        <img class="svc-img" src="images/2aoboqwjpcphf2q485jx04hoiq3ceyb1tag0qavc7.jpg"
             alt="Tư thế yoga nhóm nhỏ — side-lying leg extension">
        <div class="svc-body">
          <div class="svc-num">02 · Group</div>
          <div class="svc-title">Small Group 1:6</div>
          <p class="svc-desc">Lớp nhỏ tối đa 6 người — năng lượng nhóm kết hợp sự chú ý cá nhân. Không khí ấm áp và cùng nhau phát triển trên thảm tập.</p>
          <a href="#contact" class="svc-cta">Đăng ký</a>
        </div>
      </div>
      <div class="svc-card">
        <img class="svc-img" src="images/2aoboqwjpekwlzw6o7y5mpyynoy5lhgvbe0esu4e12.jpg"
             alt="Yoga instruction in English — side bend pose">
        <div class="svc-body">
          <div class="svc-num">03 · English</div>
          <div class="svc-title">English Instruction</div>
          <p class="svc-desc">Giảng dạy hoàn toàn bằng tiếng Anh — alignment cues và feedback rõ ràng. Thân thiện với học viên quốc tế tại TP.HCM.</p>
          <a href="#contact" class="svc-cta">Đăng ký</a>
        </div>
      </div>
      <div class="svc-card">
        <img class="svc-img" src="images/2aoboqwjpf3xjsj5gzhisjfq6zc9faot9e6muyiq14.jpg"
             alt="Yoga tại địa điểm linh hoạt — sphinx pose"
             style="object-position: center 35%;">
        <div class="svc-body">
          <div class="svc-num">04 · Location</div>
          <div class="svc-title">Linh hoạt địa điểm</div>
          <p class="svc-desc">Tại studio, tại nhà học viên hoặc ngoài trời. Trải nghiệm tập luyện thoải mái nhất trong không gian bạn chọn.</p>
          <a href="#contact" class="svc-cta">Đăng ký</a>
        </div>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Verify in browser**

Open `http://localhost:8890/index.html`, scroll to Services. Check:
- Cream background, centered heading
- 2×2 grid of cards with real photos loading
- Cards have title, description, brown "Đăng ký →" link
- Hover lifts card slightly
- On mobile: single column

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: services section with photo cards"
```

---

### Task 4: About section

**Files:**
- Modify: `index.html` — add about CSS and HTML

- [ ] **Step 1: Add about CSS**

Add inside `<style>`:

```css
/* ── ABOUT ── */
.about { background: var(--black); padding: 0; }
.about-split { display: grid; grid-template-columns: 1fr 1fr; min-height: 620px; }
.about-photo { overflow: hidden; }
.about-photo img {
  width: 100%; height: 100%;
  object-fit: cover; object-position: center top; display: block;
}
.about-content {
  padding: 80px 64px;
  display: flex; flex-direction: column; justify-content: center;
}
.about-content .s-eye { color: var(--brown); }
.about-content .s-head { color: var(--white); margin-bottom: 24px; }
.about-quote {
  font-size: 15px; font-style: italic; font-weight: 300;
  color: rgba(255,255,255,0.55); line-height: 1.75;
  border-left: 2px solid var(--brown); padding-left: 20px; margin-bottom: 24px;
}
.about-body {
  font-size: 14px; color: rgba(255,255,255,0.5); line-height: 1.9; margin-bottom: 12px;
}
.about-tags { display: flex; flex-wrap: wrap; gap: 8px; margin-top: 24px; }
.about-tag {
  font-size: 11px; font-weight: 500; letter-spacing: 0.06em; text-transform: uppercase;
  color: rgba(255,255,255,0.65); border: 1px solid rgba(255,255,255,0.15);
  padding: 5px 14px; border-radius: 9999px;
}
.cert-row {
  display: flex; gap: 14px; align-items: flex-start;
  margin-top: 20px; padding-top: 20px;
  border-top: 1px solid rgba(255,255,255,0.08);
}
.cert-icon { font-size: 18px; flex-shrink: 0; margin-top: 2px; }
.cert-title { font-size: 13px; font-weight: 500; color: rgba(255,255,255,0.8); margin-bottom: 3px; }
.cert-sub { font-size: 12px; color: rgba(255,255,255,0.35); }

@media (max-width: 768px) {
  .about-split { grid-template-columns: 1fr; }
  .about-photo { min-height: 360px; }
  .about-content { padding: 48px 24px; }
}
```

- [ ] **Step 2: Add about HTML**

After the services `</section>`:

```html
<!-- ABOUT -->
<section class="about" id="about">
  <div class="about-split">
    <div class="about-photo">
      <img src="images/2aoboqwjpelzb93t9tnogm1sgfkuivyl9txvhwbi13.jpg"
           alt="Thạch Thảo — yoga instructor, back view">
    </div>
    <div class="about-content">
      <p class="s-eye">Về tôi</p>
      <h2 class="s-head s-head-light">Khỏe · Đẹp ·<br><strong>Bền vững</strong></h2>
      <blockquote class="about-quote">
        "Cơ thể mỗi người đều có câu chuyện riêng — tôi ở đây để lắng nghe và đồng hành."
      </blockquote>
      <p class="about-body">
        Thạch Thảo là Yoga &amp; Movement Instructor với chuyên môn sâu về giải phẫu học ứng dụng và somatic movement. Cách tiếp cận tập luyện đặt alignment, breath control và kết nối cơ thể — tâm trí lên hàng đầu.
      </p>
      <p class="about-body">
        Giảng dạy bằng cả <strong style="color:rgba(255,255,255,0.8)">tiếng Việt và tiếng Anh</strong>, chào đón học viên trong nước lẫn quốc tế tại TP.HCM. Mỗi buổi học được thiết kế riêng cho từng người.
      </p>
      <div class="about-tags">
        <span class="about-tag">Alignment</span>
        <span class="about-tag">Breath Work</span>
        <span class="about-tag">Somatic</span>
        <span class="about-tag">Anatomy</span>
        <span class="about-tag">English</span>
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
</section>
```

- [ ] **Step 3: Verify in browser**

Scroll to About section. Check:
- Black background, no padding (photo flush to edges)
- Left: back-view photo fills the panel top to bottom
- Right: white heading, brown-bordered quote, faded body text, pill tags, cert rows with border-top separators
- On mobile: stacks with photo on top (360px min height)

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: about section with dark split layout and photo"
```

---

### Task 5: Strengths section

**Files:**
- Modify: `index.html` — add strengths CSS and HTML

- [ ] **Step 1: Add strengths CSS**

Add inside `<style>`:

```css
/* ── STRENGTHS ── */
.strengths { background: var(--white); }
.strengths-grid {
  display: grid; grid-template-columns: repeat(4, 1fr);
  gap: 1px; background: var(--border);
  border: 1px solid var(--border); border-radius: 12px; overflow: hidden;
  margin-top: 48px;
}
.str-item { background: var(--white); padding: 36px 24px; }
.str-num {
  font-size: 40px; font-weight: 300; color: var(--border-m);
  line-height: 1; margin-bottom: 20px;
}
.str-title {
  font-size: 11px; font-weight: 700; letter-spacing: 0.14em;
  text-transform: uppercase; color: var(--text); margin-bottom: 10px;
}
.str-body { font-size: 13px; color: var(--faint); line-height: 1.75; }

@media (max-width: 768px) {
  .strengths-grid { grid-template-columns: 1fr; }
}
```

- [ ] **Step 2: Add strengths HTML**

After the about `</section>`:

```html
<!-- STRENGTHS -->
<section class="strengths" id="strengths">
  <div class="inner">
    <p class="s-eye">Thế mạnh</p>
    <h2 class="s-head">Điều em <strong>mang lại</strong></h2>
    <div class="strengths-grid">
      <div class="str-item">
        <div class="str-num">01</div>
        <div class="str-title">Movement & Somatic</div>
        <p class="str-body">Am hiểu giải phẫu học ứng dụng, kiểm soát chuyển động và nhịp thở phù hợp với từng cơ thể, từng giai đoạn sức khỏe.</p>
      </div>
      <div class="str-item">
        <div class="str-num">02</div>
        <div class="str-title">Alignment Precision</div>
        <p class="str-body">Căn chỉnh định tuyến chuẩn xác trong từng tư thế — giảm thiểu chấn thương và tối ưu hiệu quả của từng buổi tập.</p>
      </div>
      <div class="str-item">
        <div class="str-num">03</div>
        <div class="str-title">Personalized Journey</div>
        <p class="str-body">Xây dựng lộ trình cá nhân hóa dựa trên sự thấu cảm — lắng nghe trước, hướng dẫn sau.</p>
      </div>
      <div class="str-item">
        <div class="str-num">04</div>
        <div class="str-title">Kết nối & Sáng tạo</div>
        <p class="str-body">Giao tiếp thân thiện, năng lượng tích cực và khả năng chụp ảnh lưu giữ hành trình — mỗi buổi tập là một kỷ niệm.</p>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Verify in browser**

Scroll to Strengths. Check:
- White background, 4-column bordered grid on desktop
- Large light-gray numbers, bold uppercase titles, faint body text
- 1px gap lines between cells forming the grid border effect
- On mobile: single column stack

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: strengths section with numbered bordered grid"
```

---

### Task 6: Journey section

**Files:**
- Modify: `index.html` — add journey CSS and HTML

- [ ] **Step 1: Add journey CSS**

Add inside `<style>`:

```css
/* ── JOURNEY ── */
.journey { background: var(--black); }
.journey .s-eye { color: var(--brown); }
.journey .s-head { color: var(--white); }
.journey-grid {
  display: grid; grid-template-columns: 1fr 1fr;
  gap: 80px; margin-top: 48px; align-items: start;
}
.tl-item { display: flex; gap: 20px; margin-bottom: 36px; }
.tl-dot-col {
  display: flex; flex-direction: column; align-items: center; padding-top: 5px;
}
.tl-dot {
  width: 8px; height: 8px; background: var(--brown);
  border-radius: 50%; flex-shrink: 0;
}
.tl-line {
  width: 1px; background: rgba(255,255,255,0.07);
  flex: 1; margin-top: 8px; min-height: 28px;
}
.tl-date {
  font-size: 10px; font-weight: 600; letter-spacing: 0.15em;
  text-transform: uppercase; color: var(--brown); margin-bottom: 4px;
}
.tl-title { font-size: 16px; font-weight: 500; color: var(--white); margin-bottom: 4px; }
.tl-sub { font-size: 12px; color: rgba(255,255,255,0.35); }
.metrics-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
.m-card {
  background: rgba(255,255,255,0.04);
  border: 1px solid rgba(255,255,255,0.07);
  border-radius: 10px; padding: 28px; text-align: center;
}
.m-val {
  font-size: 38px; font-weight: 300; color: var(--white); line-height: 1; margin-bottom: 8px;
}
.m-lbl { font-size: 12px; color: rgba(255,255,255,0.35); line-height: 1.5; }

@media (max-width: 768px) {
  .journey-grid { grid-template-columns: 1fr; gap: 48px; }
}
```

- [ ] **Step 2: Add journey HTML**

After the strengths `</section>`:

```html
<!-- JOURNEY -->
<section class="journey" id="journey">
  <div class="inner">
    <p class="s-eye">Hành trình</p>
    <h2 class="s-head s-head-light">Kinh nghiệm &amp; <strong>Thành tích</strong></h2>
    <div class="journey-grid">
      <div>
        <div class="tl-item">
          <div class="tl-dot-col"><div class="tl-dot"></div><div class="tl-line"></div></div>
          <div>
            <div class="tl-date">06.2025 — Hiện tại</div>
            <div class="tl-title">Yoga Instructor</div>
            <div class="tl-sub">Private 1:1 &amp; Small Group · TP.HCM</div>
          </div>
        </div>
        <div class="tl-item">
          <div class="tl-dot-col"><div class="tl-dot"></div><div class="tl-line"></div></div>
          <div>
            <div class="tl-date">2024</div>
            <div class="tl-title">200h YTT Certificate</div>
            <div class="tl-sub">Yoga Alliance · Chứng nhận quốc tế</div>
          </div>
        </div>
        <div class="tl-item">
          <div class="tl-dot-col"><div class="tl-dot"></div><div class="tl-line"></div></div>
          <div>
            <div class="tl-date">2022 — 2025</div>
            <div class="tl-title">Marketing Executive (Team Lead)</div>
            <div class="tl-sub">Wellness Brand · Tăng 20% tương tác cảm xúc</div>
          </div>
        </div>
        <div class="tl-item">
          <div class="tl-dot-col"><div class="tl-dot"></div></div>
          <div>
            <div class="tl-date">2024</div>
            <div class="tl-title">Cử nhân Marketing</div>
            <div class="tl-sub">Đại học Tôn Đức Thắng</div>
          </div>
        </div>
      </div>
      <div>
        <div class="metrics-grid">
          <div class="m-card">
            <div class="m-val">70%</div>
            <div class="m-lbl">Tỷ lệ học viên tái đăng ký</div>
          </div>
          <div class="m-card">
            <div class="m-val">–30%</div>
            <div class="m-lbl">Đau mỏi hệ vận động sau 10 buổi</div>
          </div>
          <div class="m-card">
            <div class="m-val">+20%</div>
            <div class="m-lbl">Tương tác cảm xúc thương hiệu</div>
          </div>
          <div class="m-card">
            <div class="m-val">0</div>
            <div class="m-lbl">Chấn thương trong quá trình dạy</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 3: Verify in browser**

Scroll to Journey. Check:
- Black background, brown dots and date labels in timeline
- Connecting lines between all items except the last
- Right column: 2×2 metrics grid with large numbers
- On mobile: timeline stacks above metrics

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: journey section with timeline and metrics grid"
```

---

### Task 7: CTA Band, Contact, and Footer

**Files:**
- Modify: `index.html` — add remaining CSS and HTML

- [ ] **Step 1: Add CTA band, contact, and footer CSS**

Add inside `<style>`:

```css
/* ── CTA BAND ── */
.cta-band { background: var(--brown); padding: 88px 5vw; text-align: center; }
.cta-band .s-head {
  color: var(--white); max-width: 600px;
  margin-left: auto; margin-right: auto; margin-bottom: 16px;
}
.cta-band .s-sub {
  color: rgba(255,255,255,0.8);
  margin-left: auto; margin-right: auto; margin-bottom: 32px; text-align: center;
}
.cta-band-btn {
  display: inline-block; background: var(--white); color: var(--brown);
  padding: 14px 34px; border-radius: 9999px;
  font-size: 13px; font-weight: 700; letter-spacing: 0.08em; text-transform: uppercase;
  text-decoration: none; transition: opacity 200ms;
}
.cta-band-btn:hover { opacity: 0.9; }
.cta-band-btn:focus-visible { outline: 2px solid var(--white); outline-offset: 4px; }

/* ── CONTACT ── */
.contact { background: var(--cream); }
.contact-grid {
  display: grid; grid-template-columns: 1fr 1fr;
  gap: 80px; align-items: center; margin-top: 48px;
}
.contact-row {
  display: flex; gap: 14px; align-items: center;
  color: var(--muted); font-size: 14px; font-weight: 300;
  text-decoration: none; margin-bottom: 16px; transition: color 200ms;
}
.contact-row:hover { color: var(--text); }
.contact-row:focus-visible { outline: 2px solid var(--brown); outline-offset: 4px; border-radius: 4px; }
.c-icon {
  width: 40px; height: 40px; background: var(--white); border: 1px solid var(--border);
  border-radius: 50%; display: flex; align-items: center; justify-content: center;
  font-size: 15px; flex-shrink: 0;
}
.social-row { display: flex; gap: 10px; margin-top: 24px; }
.soc-btn {
  width: 40px; height: 40px; border: 1px solid var(--border-m); border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  color: var(--faint); text-decoration: none;
  font-size: 10px; font-weight: 600; letter-spacing: 0.05em; transition: all 200ms;
}
.soc-btn:hover { border-color: var(--brown); color: var(--brown); }
.soc-btn:focus-visible { outline: 2px solid var(--brown); outline-offset: 4px; }
.contact-cta-box { background: var(--black); border-radius: 24px; padding: 44px; }
.contact-cta-q {
  font-size: 22px; font-weight: 300; font-style: italic;
  color: var(--white); line-height: 1.45; margin-bottom: 16px;
}
.contact-cta-p {
  font-size: 13px; color: rgba(255,255,255,0.5); line-height: 1.85; margin-bottom: 28px;
}
.contact-cta-btn {
  display: inline-block; background: var(--white); color: var(--black);
  padding: 13px 26px; border-radius: 9999px;
  font-size: 13px; font-weight: 700; text-decoration: none; transition: opacity 200ms;
}
.contact-cta-btn:hover { opacity: 0.88; }
.contact-cta-btn:focus-visible { outline: 2px solid var(--white); outline-offset: 4px; }

/* ── FOOTER ── */
footer {
  background: var(--black);
  border-top: 1px solid rgba(255,255,255,0.07);
  padding: 28px 5vw;
}
.footer-inner {
  max-width: 1100px; margin: 0 auto;
  display: flex; justify-content: space-between; align-items: center;
  flex-wrap: wrap; gap: 16px;
}
.footer-brand { font-size: 14px; font-weight: 600; color: var(--white); letter-spacing: 0.06em; }
.footer-tag { font-size: 11px; color: rgba(255,255,255,0.28); margin-top: 4px; font-style: italic; }
.footer-links { display: flex; gap: 24px; }
.footer-links a {
  font-size: 11px; color: rgba(255,255,255,0.35); text-decoration: none;
  letter-spacing: 0.06em; text-transform: uppercase;
}
.footer-links a:hover { color: rgba(255,255,255,0.7); }
.footer-copy { font-size: 11px; color: rgba(255,255,255,0.22); }

@media (max-width: 768px) {
  .contact-grid { grid-template-columns: 1fr; gap: 40px; }
  .footer-inner { flex-direction: column; align-items: flex-start; }
}

/* ── REDUCED MOTION ── */
@media (prefers-reduced-motion: reduce) {
  .svc-card, .hero-btn, .nav-cta, .cta-band-btn { transition: none; }
  .svc-card:hover { transform: none; }
}
```

- [ ] **Step 2: Add CTA band, contact, and footer HTML**

After the journey `</section>`, add:

```html
<!-- CTA BAND -->
<section class="cta-band">
  <div class="inner">
    <h2 class="s-head">Sẵn sàng bắt đầu<br><strong>hành trình của bạn?</strong></h2>
    <p class="s-sub">Dù mới bắt đầu, đang phục hồi chấn thương, hay muốn đi sâu hơn — em ở đây để đồng hành cùng bạn.</p>
    <a href="#contact" class="cta-band-btn">Đặt buổi học thử miễn phí</a>
  </div>
</section>

<!-- CONTACT -->
<section class="contact" id="contact">
  <div class="inner">
    <p class="s-eye">Liên hệ</p>
    <h2 class="s-head">Kết nối <strong>cùng Thảo</strong></h2>
    <div class="contact-grid">
      <div>
        <a href="tel:0703786631" class="contact-row">
          <div class="c-icon">📞</div><span>0703 786 631</span>
        </a>
        <a href="mailto:thachdua29@gmail.com" class="contact-row">
          <div class="c-icon">✉</div><span>thachdua29@gmail.com</span>
        </a>
        <a href="https://www.facebook.com/dua.thach.2906/" target="_blank" rel="noopener" class="contact-row">
          <div class="c-icon">f</div><span>Facebook: dua.thach.2906</span>
        </a>
        <a href="https://www.instagram.com/thach_dua/" target="_blank" rel="noopener" class="contact-row">
          <div class="c-icon">ig</div><span>Instagram: @thach_dua</span>
        </a>
        <a href="https://www.threads.com/@thach_dua" target="_blank" rel="noopener" class="contact-row">
          <div class="c-icon">t</div><span>Threads: @thach_dua</span>
        </a>
        <div class="social-row">
          <a href="https://www.facebook.com/dua.thach.2906/" target="_blank" rel="noopener" class="soc-btn" aria-label="Facebook">FB</a>
          <a href="https://www.instagram.com/thach_dua/" target="_blank" rel="noopener" class="soc-btn" aria-label="Instagram">IG</a>
          <a href="https://www.threads.com/@thach_dua" target="_blank" rel="noopener" class="soc-btn" aria-label="Threads">TH</a>
        </div>
      </div>
      <div class="contact-cta-box">
        <div class="contact-cta-q">"Hành trình ngàn dặm bắt đầu từ một hơi thở."</div>
        <p class="contact-cta-p">Dù bạn mới bắt đầu, đang phục hồi chấn thương, hay muốn đi sâu hơn vào thực hành — em ở đây để đồng hành cùng bạn. Liên hệ để đặt buổi học thử miễn phí.</p>
        <a href="mailto:thachdua29@gmail.com" class="contact-cta-btn">Đặt buổi học thử →</a>
      </div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-inner">
    <div>
      <div class="footer-brand">Thạch Thảo</div>
      <div class="footer-tag">Bắt nguồn từ cơ thể. Chuyển hóa qua chuyển động.</div>
    </div>
    <nav class="footer-links" aria-label="Footer navigation">
      <a href="#services">Dịch vụ</a>
      <a href="#about">Giới thiệu</a>
      <a href="#journey">Hành trình</a>
      <a href="#contact">Liên hệ</a>
    </nav>
    <div class="footer-copy">© 2025 Nguyễn Thạch Thảo · TP. Hồ Chí Minh</div>
  </div>
</footer>
```

- [ ] **Step 3: Verify in browser**

Scroll through bottom of page. Check:
- Brown CTA band with white button "Đặt buổi học thử miễn phí"
- Cream contact section: left column with contact rows + social buttons, right column with dark CTA box
- Dark footer: brand + tagline left, nav links center, copyright right
- Social buttons show `aria-label` (inspect in DevTools → Accessibility)
- All external links have `rel="noopener"`
- On mobile: contact grid stacks, footer stacks

- [ ] **Step 4: Full page check**

Tab through the entire page with keyboard. Check:
- Every interactive element (nav links, hero CTA, service CTAs, contact links, social buttons, footer links) shows a visible focus ring
- `scroll-margin-top: 64px` ensures nav links scroll to the right position without content hidden behind fixed nav

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: CTA band, contact section, footer, and accessibility polish"
```

---

### Task 8: Cleanup

**Files:**
- Delete: `mockup-preview.html`
- Modify: `.gitignore`

- [ ] **Step 1: Add .superpowers to .gitignore**

```bash
echo ".superpowers/" >> .gitignore
git add .gitignore
```

- [ ] **Step 2: Delete temp mockup file**

```bash
git rm mockup-preview.html
```

- [ ] **Step 3: Final visual QA**

Open `http://localhost:8890/index.html`. Run through this checklist:

- [ ] Hero photo loads, overlay visible, stats bar at bottom
- [ ] "Xem dịch vụ" button scrolls to #services with correct offset
- [ ] All 4 service card photos load (not broken images)
- [ ] About photo loads on the left, content on right
- [ ] Strengths grid has visible border lines between cells
- [ ] Journey timeline has brown dots and connecting lines
- [ ] CTA band is warm brown, not black or cream
- [ ] Contact section: all 5 contact rows display, social buttons show
- [ ] Footer: 3 columns visible on desktop
- [ ] Resize to mobile width (≤768px): nav links hidden, all grids single column
- [ ] Open Network tab in DevTools: no 404 errors for images

- [ ] **Step 4: Final commit**

```bash
git commit -m "chore: remove temp mockup file, add .superpowers to .gitignore"
```

---

## Self-Review Notes

- All 8 sections from spec are covered: Nav, Hero, Services, About, Strengths, Journey, CTA Band, Contact + Footer
- All image filenames match the `images/` directory exactly
- `rel="noopener"` added to all `target="_blank"` links (security)
- `prefers-reduced-motion` added in Task 7
- `aria-label` on icon-only social buttons
- `scroll-margin-top: 64px` on all `section` elements covers the fixed nav height
- `focus-visible` rules present on all interactive elements
