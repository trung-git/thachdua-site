# Thạch Thảo Site Redesign Spec
**Date:** 2026-05-16  
**Reference design:** courtneywatts.com  
**Approved mockup:** `mockup-preview.html`

---

## Context & Goals

Redesign the single-page personal website for Nguyễn Thạch Thảo (Yoga & Movement Instructor) using the Courtney Watts Studio visual system. The goal is a polished, photo-forward marketing site that converts visitors into students.

**Target file:** `index.html` (single self-contained HTML file, no build step)  
**Images:** `images/` folder, 15 studio photos already available

---

## Design Decisions

| Decision | Choice | Rationale |
|---|---|---|
| Overall palette | Light + Dark Contrast (Option C) | Cream body, dark feature blocks, alternating rhythm |
| Hero | Full-width editorial (Option A) | Content-first, no image split — photo as full-bleed background |
| Sections | All 6 kept (Option A) | Complete portfolio, detailed credentials |

---

## Design Tokens

```css
--black: #000000;          /* surface.base */
--cream: #f8f6f2;          /* surface.raised */
--brown: #8a7b67;          /* surface.strong — accent, eyebrows, CTAs */
--text:  #1f2937;          /* text.primary */
--muted: #4b5563;          /* text.tertiary */
--faint: #6b7280;          /* text.inverse */
--border: #e5e7eb;         /* border.default */
--border-m: #d1d5db;       /* border.muted */
--white: #ffffff;
```

**Font:** Poppins (300, 400, 500, 600, 700, italic variants) via Google Fonts  
**Base size:** 16px, weight 300, line-height 24px

**Spacing scale (px):** 8 · 12 · 16 · 20 · 24 · 32 · 64 · 96  
**Radius:** xs=6 · sm=10 · md=12 · lg=24 · xl=50 · pill=9999px  
**Motion:** instant=150ms · fast=200ms · normal=300ms

---

## Page Sections

### 1. Nav (fixed, dark)
- Background: `rgba(0,0,0,0.72)` + `backdrop-filter: blur(16px)`
- Height: 64px, padding: 0 5vw
- Logo: Poppins 600, 16px, uppercase, white
- Links: 12px, 400, uppercase, letter-spacing 0.1em, `rgba(255,255,255,0.7)` → white on hover
- CTA button: white bg, black text, pill radius, 12px 700 uppercase — links to `#contact`
- Mobile: nav links hidden, logo + CTA only

### 2. Hero (full-bleed image, dark overlay)
- Height: 100vh, `min-height: 640px`
- Background image: `images/2aoboqwjpbpxuohyoxawbfhjyfrezbrump8bomac4.jpg`
  - `background-size: cover; background-position: center 20%`
  - Overlay: `linear-gradient(to bottom, rgba(0,0,0,0.4) 0%, rgba(0,0,0,0.62) 60%, rgba(0,0,0,0.82) 100%)`
- Content (centered, z-index 1, max-width 740px):
  - Eyebrow: 11px, 500, letter-spacing 0.25em, uppercase, `--brown`
  - H1: `clamp(44px, 7vw, 82px)`, weight 300, line-height 1.0, white. Name on first line (300), "Thạch Thảo" on second (700 strong block)
  - Tagline: `clamp(14px, 1.6vw, 17px)`, italic 300, `rgba(255,255,255,0.65)`
  - CTA button: white bg, black text, pill, 13px 700 uppercase — links to `#services`
- Stats bar (pinned bottom):
  - `rgba(0,0,0,0.55)` + `backdrop-filter: blur(12px)`
  - 3 columns with dividers: 200h YTT · 70% tái đăng ký · –30% đau mỏi
  - Value: 26px 300 white | Label: 10px 500 uppercase `rgba(255,255,255,0.38)`

### 3. Services (cream bg, photo cards)
- Background: `--cream`
- Header: centered eyebrow + heading + subtitle
- Grid: 2×2, gap 20px
- Card anatomy:
  - Image: `height: 240px`, `object-fit: cover`
  - Body padding: 24px 26px
  - Number label: 10px 600 `--brown` uppercase
  - Title: 19px 600 `--text`
  - Description: 13px 400 `--muted`, line-height 1.8
  - CTA link: 12px 600 `--brown` uppercase + " →", links to `#contact`
  - Hover: `translateY(-3px)` + shadow
- Image assignments:
  - 01 Private: `...c2wkuicbem...6.jpg` (object-position: center 30%)
  - 02 Small Group: `...cphf2q485...7.jpg`
  - 03 English: `...ekwlzw6o7...12.jpg`
  - 04 Location: `...f3xjsj5gz...14.jpg` (object-position: center 35%)

### 4. About (dark split, photo left)
- Background: `--black`, padding: 0
- Grid: `1fr 1fr`, min-height: 620px
- Left: photo `...elzb93t9t...13.jpg` — `object-fit: cover; object-position: center top`
- Right content (padding: 80px 64px):
  - Eyebrow: `--brown`
  - H2: white, weight 300 / 700
  - Blockquote: 15px italic 300, `rgba(255,255,255,0.55)`, left border 2px `--brown`
  - Body text: 14px `rgba(255,255,255,0.5)`, line-height 1.9
  - Skill tags: pill border `rgba(255,255,255,0.15)`, text `rgba(255,255,255,0.65)`, 11px 500 uppercase
  - Cert rows: border-top `rgba(255,255,255,0.08)`, icon + title (13px 500 `rgba(255,255,255,0.8)`) + sub (12px `rgba(255,255,255,0.35)`)
- Mobile: stack vertically, photo 360px min-height, content padding 48px 24px

### 5. Strengths (white bg, bordered grid)
- Background: `--white`
- Grid: 4 columns, 1px gap, border `--border`, border-radius 12px, overflow hidden
- Each cell: white bg, padding 36px 24px
  - Number: 40px 300 `--border-m`
  - Title: 11px 700 uppercase letter-spacing 0.14em `--text`
  - Body: 13px `--faint`, line-height 1.75

### 6. Journey (dark bg, timeline + metrics)
- Background: `--black`
- Grid: `1fr 1fr`, gap 80px
- Timeline (left): dot (`--brown`, 8px) + vertical line (`rgba(255,255,255,0.07)`)
  - Date: 10px 600 uppercase `--brown`
  - Title: 16px 500 white
  - Sub: 12px `rgba(255,255,255,0.35)`
- Metrics grid (right): 2×2
  - Card: `rgba(255,255,255,0.04)` bg, border `rgba(255,255,255,0.07)`, radius 10px
  - Value: 38px 300 white | Label: 12px `rgba(255,255,255,0.35)`

### 7. CTA Band (brown bg)
- Background: `--brown`, padding 88px 5vw, text-align center
- H2: white 300/700, centered, max-width 600px
- Subtitle: `rgba(255,255,255,0.8)`, centered
- Button: white bg, `--brown` text, pill, 13px 700 uppercase — links to `#contact`

### 8. Contact (cream bg)
- Background: `--cream`
- Grid: `1fr 1fr`, gap 80px
- Left: contact rows (phone, email, Facebook, Instagram, Threads) + social icon buttons
  - Row: icon circle (white bg, border `--border`, 40px) + text `--muted` 14px
  - Social buttons: 40px circle, border `--border-m`, 10px 600, hover → `--brown`
- Right: dark CTA box
  - Background: `--black`, border-radius 24px, padding 44px
  - Quote: 22px italic 300 white
  - Body: 13px `rgba(255,255,255,0.5)`
  - Button: white bg, black text, pill, 13px 700 — `mailto:thachdua29@gmail.com`

### 9. Footer (dark)
- Background: `--black`, border-top `rgba(255,255,255,0.07)`, padding 28px 5vw
- 3-column flex: brand+tagline · nav links · copyright
- Brand: 14px 600 white uppercase | Tagline: 11px italic `rgba(255,255,255,0.28)`
- Links: 11px uppercase `rgba(255,255,255,0.35)` → 0.7 on hover
- Copy: 11px `rgba(255,255,255,0.22)`

---

## Accessibility (WCAG 2.2 AA)

- All nav links must have `:focus-visible` outline
- Hero CTA must have minimum 4.5:1 contrast ratio (white on dark overlay — passes)
- Service card CTAs must be distinguishable without color alone
- `alt` text required on all images (describe pose, not filename)
- Fixed nav must not obscure scroll targets — use `scroll-margin-top: 64px` on all section IDs
- `prefers-reduced-motion`: disable `translateY` hover and any future scroll animations

---

## Responsive Breakpoint (≤768px)

- Nav: hide links, show logo + CTA only
- Hero: `min-height: 100svh`
- Services grid: 1 column
- About split: stack vertically (photo 360px → content)
- Strengths grid: 1 column
- Journey grid: 1 column
- Contact grid: 1 column
- Footer: stack vertically

---

## Content

All content is Vietnamese. Contact:
- Phone: 0703 786 631
- Email: thachdua29@gmail.com
- Facebook: facebook.com/dua.thach.2906/
- Instagram: @thach_dua
- Threads: @thach_dua

---

## Implementation Notes

- Single `index.html` file, no build step, no external dependencies except Google Fonts
- Replace existing `index.html` entirely
- `mockup-preview.html` is the approved reference — can be deleted after implementation
- `.superpowers/` should be added to `.gitignore`
