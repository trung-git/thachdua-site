# Thạch Dừa Studio — Site Design Spec

**Date:** 2026-05-16  
**Reference:** courtneywatts.com (faithful multi-page clone)  
**Subject:** Nguyễn Thạch Thảo — Yoga & Movement Instructor, TP. Hồ Chí Minh

---

## 1. Overview

A faithful, multi-page clone of the Courtney Watts Studio site, adapted for Thạch Thảo's brand "Thạch Dừa Studio." Visual design, layout, and typography follow CWS exactly. Content is Thạch Thảo's — bilingual Vietnamese + English throughout.

**Pages:**
- `index.html` — Home
- `programs.html` — Programs (3 service cards)
- `about.html` — Meet Thạch Thảo
- `pricing.html` — Pricing
- `style.css` — Shared stylesheet across all pages

---

## 2. Brand & Identity

| Property | Value |
|----------|-------|
| **Studio name** | Thạch Dừa Studio |
| **Instructor** | Nguyễn Thạch Thảo |
| **Tagline** | Bắt nguồn từ cơ thể. Powered by movement. |
| **Disciplines** | Yoga · Movement · Somatic |
| **Location** | TP. Hồ Chí Minh |
| **Contact** | thachdua29@gmail.com · 0703 786 631 |
| **Social** | Instagram @thach_dua · Facebook dua.thach.2906 · Threads @thach_dua |

**Logo mark:** "Thạch Dừa Studio" in Playfair Display (400 weight), with "Movement & Somatic" in small caps (Inter 600, 0.28em letter-spacing, taupe) on the line below.

---

## 3. Design System

### Colors

```css
--white:   #ffffff
--cream:   #faf7f3
--taupe:   #8b704f   /* accent: buttons, labels, eyebrows, logo sub */
--charcoal:#1a1a1a   /* primary text */
--muted:   #888888   /* body copy, descriptions */
--border:  #e8e2d9
```

No pure black sections. All page backgrounds are white or cream.

### Typography

| Role | Font | Weight | Notes |
|------|------|--------|-------|
| Headings | Playfair Display | 400 / italic 400 | Section titles, hero h1, card titles |
| Eyebrows | Inter | 600 | 10–11px, 0.22–0.28em letter-spacing, uppercase, taupe |
| Body | Inter | 300–400 | 13–15px, 1.7–1.85 line-height |
| Nav links | Inter | 400 | 13px |
| Buttons | Inter | 600 | 12px, 0.06em letter-spacing |

### Spacing

- Max content width: `1100px`, centered
- Section padding: `96px 5vw`
- Nav height: `72px`

---

## 4. Shared Components

### Navigation (all pages)

```
[Thạch Dừa Studio]     Dịch vụ   Giới thiệu   Bảng giá     [Đặt lịch ngay]
     logo (left)            center links               taupe pill CTA (right)
```

- Background: `#ffffff`, `border-bottom: 1px solid #eee`
- Logo: Playfair Display 17px + Inter small caps sub-label in taupe
- Links: Inter 13px, color `#444`, no transform
- CTA button: `background: #8b704f`, white text, `border-radius: 9999px`, `padding: 10px 22px`
- Fixed/sticky on scroll

### Footer (all pages)

Dark background `#1a1a1a`, 4-column grid:

| Col 1 | Col 2 | Col 3 | Col 4 |
|-------|-------|-------|-------|
| Thạch Dừa Studio (brand) | Studio links | Connect | Contact Us |
| Tagline (italic, muted) | Dịch vụ · Giới thiệu · Bảng giá | Instagram · Facebook · Threads | Email · Phone |

Bottom: `© 2025 Thạch Dừa Studio · TP. Hồ Chí Minh`

---

## 5. Page Specs

### 5.1 index.html — Home

**Sections in order:**

#### Hero
- Full-screen (100vh), photo background
- **Image:** `images/2aoboqwjpbpxuohyoxawbfhjyfrezbrump8bomac4.jpg`
- Gradient overlay: `linear-gradient(to left, rgba(0,0,0,0.65) 0%, rgba(0,0,0,0.25) 55%, transparent 100%)`
- Text block: right-aligned, `padding: 0 72px`, `max-width: 580px`
  - Eyebrow: "Yoga · Movement · Somatic — TP. Hồ Chí Minh"
  - H1 (Playfair 400): "Welcome to / *Thạch Dừa* / Studio" (name line in italic)
  - Tagline: "Bắt nguồn từ cơ thể. / Powered by movement." (italic, muted)
  - CTA button: "Explore Programs" — outline pill (semi-transparent white border, backdrop-blur)

#### Programs preview
- Eyebrow: "EXPLORE OUR PROGRAMS"
- H2: "Programs"
- Sub: "Chọn hình thức phù hợp với cơ thể, mục tiêu và lịch trình của bạn."
- 3 cards (same as programs.html) with "Learn More →" linking to `programs.html`
- Background: `#ffffff`

#### Testimonials
- Eyebrow: "WHAT PEOPLE ARE SAYING"
- H2: "What Our Students Say"
- Sub: "Discover how Thảo's students have transformed their practice."
- Carousel of 5 review cards (see §6 for content)
- Background: `#faf7f3`

#### CTA / Email signup
- Background: `#8b704f`
- H2 (white): "Ready to start your wellness journey?"
- Sub: "Đặt buổi học thử miễn phí — không cam kết, không áp lực."
- Email input + "Start Today" button (white pill)

---

### 5.2 programs.html — Programs

**Sections:**

#### Page hero banner
- Tall banner (~50vh), photo background
- **Image:** `images/2aoboqwjpam0hdsjgttoadzrpmo6yn5l3ioddzjw1.jpg`
- Overlay: `rgba(0,0,0,0.45)`
- Centered text: Eyebrow "EXPLORE OUR PROGRAMS" + H1 "Programs"

#### 3 Service cards
Full-width section, `background: #ffffff`, 3-column grid, no border-radius on images (flush like CWS).

**Card 1 — Private 1:1**
- Image: `images/2aoboqwjpfn8reksp76ifyfwxgduxieminqu508o15.jpg`
- Label: PRIVATE
- Title: Private 1:1
- Lang badge: 🇻🇳 VI · 🇬🇧 EN
- Body: "Lộ trình, cường độ và mục tiêu được thiết kế hoàn toàn riêng cho bạn. Phù hợp với người mới bắt đầu hoặc đang phục hồi chấn thương."
- CTA: "Đặt lịch →" → `mailto:thachdua29@gmail.com`

**Card 2 — Small Group**
- Image: `images/2aoboqwjpcphf2q485jx04hoiq3ceyb1tag0qavc7.jpg`
- Label: GROUP
- Title: Small Group 1:6
- Lang badge: 🇻🇳 VI · 🇬🇧 EN
- Body: "Tối đa 6 người — năng lượng nhóm kết hợp sự chú ý cá nhân. Không khí ấm áp, cùng nhau phát triển trên thảm tập."
- CTA: "Đặt lịch →"

**Card 3 — Linh hoạt địa điểm**
- Image: `images/2aoboqwjpf3xjsj5gzhisjfq6zc9faot9e6muyiq14.jpg`
- Label: FLEXIBLE
- Title: Linh hoạt địa điểm
- Lang badge: 🇻🇳 VI · 🇬🇧 EN
- Body: "Tại studio, tại nhà học viên hoặc ngoài trời. Không gian thoải mái nhất cho hành trình của bạn."
- CTA: "Đặt lịch →"

**Lang badge spec:** small pill `background: rgba(255,255,255,0.92)`, taupe text, positioned bottom-left over the card image.

---

### 5.3 about.html — Meet Thạch Thảo

**Sections:**

#### About hero banner
- ~40vh banner
- **Image:** `images/2aoboqwjpelzb93t9tnogm1sgfkuivyl9txvhwbi13.jpg`
- Overlay: `rgba(0,0,0,0.4)`
- Centered: Eyebrow "ABOUT" + H1 "Meet Thạch Thảo"

#### Split bio section
- 2-column: photo left (`images/2aoboqwjpelzb93t9tnogm1sgfkuivyl9txvhwbi13.jpg`), content right
- Background: `#ffffff`

**Right column content:**
- Eyebrow: "About"
- H2: "Meet Thạch Thảo"
- Para 1: "Thạch Thảo là Yoga & Movement Instructor với chuyên môn sâu về somatic movement và giải phẫu học ứng dụng. Cách tiếp cận đặt alignment, breath control và kết nối cơ thể–tâm trí lên hàng đầu."
- Para 2: "Giảng dạy bằng cả Tiếng Việt và Tiếng Anh — thân thiện với học viên trong nước lẫn expat tại TP.HCM. Mỗi buổi học được thiết kế riêng cho từng người."
- Credential 1: ⭐ 200-Hour Yoga Teacher Training Certificate · Yoga Alliance · 2024
- Credential 2: 🎓 Cử nhân Marketing · Đại học Tôn Đức Thắng · 2024
- Tags: 🇻🇳 Tiếng Việt · 🇬🇧 English · Alignment · Somatic · Breath Work · 200h YTT · Injury Prevention

#### Secondary image accent
- Full-width image strip or floating accent
- **Image:** `images/2aoboqwjpb0izstdcjy0wo6v5sdwgmvvrkfdzyre3.jpg`
- Background: `#faf7f3`

---

### 5.4 pricing.html — Pricing

**Sections:**

#### Page hero banner
- ~40vh
- **Image:** `images/2aoboqwjpdge0szcgu1l2tpakqy9vz5xwgc1wczw9.jpg`
- Overlay: `rgba(0,0,0,0.45)`
- Centered: Eyebrow "PRICING" + H1 "Choose Your Plan"

#### Pricing cards
- Background: `#ffffff`
- Sub: "Linh hoạt theo mục tiêu — đặt lịch bất cứ lúc nào."
- 2-column grid

**Card 1 — Buổi lẻ**
- Price: 350,000 VND / buổi
- Description: "Thử một buổi không cam kết."
- Features: 1 buổi 60 phút · Private 1:1 hoặc Small Group · Tiếng Việt hoặc Tiếng Anh
- CTA: "Đặt lịch" (outline style)

**Card 2 — Gói 10 buổi ✦ Best Value** (featured/highlighted)
- Price: 2,800,000 VND / gói
- Description: "Cam kết hành trình — tiết kiệm hơn & được ưu tiên đặt lịch."
- Features: 10 buổi 60 phút · Linh hoạt hình thức & địa điểm · Tiếng Việt hoặc Tiếng Anh · Hiệu lực 3 tháng
- CTA: "Đặt lịch" (filled taupe)

#### Contact prompt
- Simple centered text: "Có câu hỏi về pricing? / Have questions about pricing?"
- Link: email → `thachdua29@gmail.com`

---

## 6. Generated Content

### Testimonials (5 reviews)

1. **Nguyễn Minh Thư** · Private 1:1 · TP.HCM ★★★★★  
   "Mình tập với Thảo được 2 tháng rồi, lưng đau mỏi giảm hẳn. Cô ấy rất chú ý đến từng tư thế và giải thích rõ tại sao phải làm đúng — không chỉ làm theo."

2. **Sarah L.** · Small Group · Ho Chi Minh City ★★★★★  
   "I was nervous joining as an expat but Thao made me feel so welcome. Her English instruction is clear and her alignment cues are incredibly precise."

3. **Trần Khánh Linh** · Linh hoạt địa điểm · TP.HCM ★★★★★  
   "Thảo dạy tại nhà mình nên không phải lo di chuyển. Buổi học rất cá nhân hóa, phù hợp với thời gian và mục tiêu của mình."

4. **James M.** · Private 1:1 · District 2 ★★★★★  
   "Thao is an exceptional teacher. She explains each movement clearly in English and I've seen incredible progress in my flexibility and core strength."

5. **Lê Phương Anh** · Small Group · TP.HCM ★★★★★  
   "Nhóm nhỏ 6 người rất ấm cúng. Thảo để ý đến từng người dù dạy nhóm — cảm giác như được học riêng vậy."

---

## 7. Image Map

| File | Used in |
|------|---------|
| `2aoboqwjpbpxuohyoxawbfhjyfrezbrump8bomac4.jpg` | Home hero |
| `2aoboqwjpam0hdsjgttoadzrpmo6yn5l3ioddzjw1.jpg` | Programs page banner |
| `2aoboqwjpfn8reksp76ifyfwxgduxieminqu508o15.jpg` | Private 1:1 card |
| `2aoboqwjpcphf2q485jx04hoiq3ceyb1tag0qavc7.jpg` | Small Group card |
| `2aoboqwjpf3xjsj5gzhisjfq6zc9faot9e6muyiq14.jpg` | Linh hoạt địa điểm card |
| `2aoboqwjpelzb93t9tnogm1sgfkuivyl9txvhwbi13.jpg` | About banner + About split photo |
| `2aoboqwjpb0izstdcjy0wo6v5sdwgmvvrkfdzyre3.jpg` | About secondary accent |
| `2aoboqwjpdge0szcgu1l2tpakqy9vz5xwgc1wczw9.jpg` | Pricing banner |

---

## 8. Responsive

- Mobile breakpoint: `768px`
- Nav: hide links, show hamburger or stack
- Hero text: centered (not right-aligned) on mobile
- Programs/pricing cards: single column
- About split: stack (photo top, content below)
- Footer: single column stack

---

## 9. File Structure

```
thachdua-site/
├── index.html
├── programs.html
├── about.html
├── pricing.html
├── style.css          ← shared nav, footer, design tokens
└── images/            ← existing folder, no changes
```
