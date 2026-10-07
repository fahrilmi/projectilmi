---
version: alpha
name: Ritme Athletic Design System
description: Kinetic sports energy meets digital precision. High-contrast athletic minimalism designed for recurring fitness communities.
colors:
  primary: "#08090A"
  surface: "#12151A"
  surface-elevated: "#1A1E24"
  border: "#242A33"
  text-primary: "#F8FAFC"
  text-secondary: "#94A3B8"
  text-muted: "#64748B"
  accent-volt: "#D4FF00"
  accent-cyan: "#00F0FF"
  accent-coral: "#FF3366"
  success: "#10B981"
typography:
  display-hero:
    fontFamily: Syne
    fontSize: "3.75rem"
    fontWeight: 800
    lineHeight: "1.05"
    letterSpacing: "-0.04em"
  display-title:
    fontFamily: Syne
    fontSize: "2.25rem"
    fontWeight: 700
    lineHeight: "1.15"
    letterSpacing: "-0.03em"
  heading-card:
    fontFamily: Plus Jakarta Sans
    fontSize: "1.25rem"
    fontWeight: 700
    lineHeight: "1.3"
    letterSpacing: "-0.02em"
  body-base:
    fontFamily: Plus Jakarta Sans
    fontSize: "1rem"
    fontWeight: 400
    lineHeight: "1.6"
  body-sm:
    fontFamily: Plus Jakarta Sans
    fontSize: "0.875rem"
    fontWeight: 500
    lineHeight: "1.5"
  mono-badge:
    fontFamily: JetBrains Mono
    fontSize: "0.75rem"
    fontWeight: 600
    letterSpacing: "0.05em"
rounded:
  sm: "6px"
  md: "12px"
  lg: "18px"
  pill: "9999px"
spacing:
  xs: "4px"
  sm: "8px"
  md: "16px"
  lg: "24px"
  xl: "48px"
  xxl: "80px"
components:
  button-primary:
    backgroundColor: "{colors.accent-volt}"
    textColor: "#08090A"
    rounded: "{rounded.pill}"
    padding: "12px 28px"
  button-primary-hover:
    backgroundColor: "#BCE000"
  button-secondary:
    backgroundColor: "{colors.surface-elevated}"
    textColor: "{colors.text-primary}"
    rounded: "{rounded.pill}"
    padding: "12px 24px"
  card-container:
    backgroundColor: "{colors.surface}"
    rounded: "{rounded.lg}"
    padding: "24px"
---

# Style Guide & Design System: RITME

## 1. Overview & Brand Archetype
RITME is an operating system for high-energy recurring fitness experiences (Poundfit, Yoga, Pilates, Running Clubs). The aesthetic is **Athletic High-Energy Meets Tactile Tech Precision**. 

### The Anti-AI Slop Manifesto
To ensure RITME never feels like generic AI-generated template sludge, we follow strict guardrails:
1. **Zero Generic AI Purples/Violets:** We reject the ubiquitous indigo-to-purple gradient. Our energy comes from authentic athletic contrasts: deep carbon obsidian canvas with **Volt Pulse (`#D4FF00`)** and sharp **Electric Cyan (`#00F0FF`)**.
2. **Zero Unearned Glassmorphism / Blur Soup:** No heavy blurry cards floating aimlessly. Surfaces have sharp tactile boundaries, crisp border lines (`#242A33`), and clear physical depth.
3. **No "Icon Topper" Repetition:** Cards do not feature identical rounded-square icons pasted mechanically above every paragraph. Information is expressed through live interactive data widgets, metrics, micro-tags, and tangible previews.
4. **Content-First Kinetic Typography:** Headlines use **Syne** with aggressive negative tracking for a punchy, athletic editorial voice. Body text relies on **Plus Jakarta Sans** for maximum scanning legibility on mobile screens.

---

## 2. Colors & Semantic Roles

| Token | Hex Value | Semantic Role & Behavior |
|---|---|---|
| `primary` / `bg` | `#08090A` | Canvas obsidian background. High-contrast, deep, and battery-friendly on OLED smartphones. |
| `surface` | `#12151A` | Card backgrounds, modular widget panels, and elevated sections. |
| `surface-elevated` | `#1A1E24` | Secondary pill buttons, hover states, interactive dropdown surfaces. |
| `border` | `#242A33` | Crisp structural borders (1px solid) defining cards and sections. |
| `accent-volt` | `#D4FF00` | Primary action driver (CTAs, active tabs, streak counters, badges). Represents athletic endorphins and vitality. |
| `accent-cyan` | `#00F0FF` | Technology indicator (AI Biometric search matches, live sync indicators). |
| `accent-coral` | `#FF3366` | Urgent alerts, cancellation notices, high-intensity milestones. |
| `text-primary` | `#F8FAFC` | Main headings, critical metrics, high-contrast readable labels. |
| `text-secondary` | `#94A3B8` | Body copy, explanatory descriptions, secondary subtitles. |
| `text-muted` | `#64748B` | Timestamp tags, table borders, inactive states, micro fine print. |

---

## 3. Typography Hierarchy

- **Display Hero (Syne 800 - 60px / -0.04em):** Bold, kinetic, and striking. Used sparingly for main headline impact.
- **Section Heading (Syne 700 - 36px / -0.03em):** Clear section dividers with an athletic rhythm.
- **Card Title (Plus Jakarta Sans 700 - 20px / -0.02em):** Legible, authoritative UI headings.
- **Body Regular (Plus Jakarta Sans 400 - 16px / 1.6):** Clean mobile readability without eye fatigue.
- **Micro / Mono (JetBrains Mono 600 - 12px / uppercase):** Used for session timestamps, QR ticket IDs, biometric match confidence (`99.4% MATCH`), and pricing tags.

---

## 4. Layout & Spacing System

- **8pt Grid Discipline:** All margins, paddings, and component dimensions adhere to multiples of 4px and 8px (8px, 16px, 24px, 32px, 48px, 80px).
- **Asymmetric Bento Grid:** Rather than 3 identical columns, dashboards and feature sections use dynamic bento hierarchy:
  - 1 Anchor Card (60% width): Live interactive module (e.g., AI Face Photo Search demo).
  - 2 Satellite Cards (40% width): Secondary metrics and micro-interactions (e.g., Streak tracker, QR check-in).

---

## 5. Elevation & Depth

- **Level 0 (Base Canvas):** Flat obsidian `#08090A`.
- **Level 1 (Card Surface):** `#12151A` with a crisp `1px solid #242A33` border.
- **Level 2 (Active/Hover Glow):** Subtle directional highlight: `box-shadow: 0 10px 30px -10px rgba(212, 255, 0, 0.12)`.
- **Level 3 (Modal/Sheet):** `#1A1E24` with backdrop blur of `rgba(8, 9, 10, 0.8)` for focus overlays.

---

## 6. Shapes & Geometry

- **Buttons & Badges:** Full Pill geometry (`border-radius: 9999px`). Tactile and thumb-friendly for quick mobile tapping.
- **Cards & Bento Cells:** Comfortable curve (`border-radius: 16px` to `18px`).
- **Interactive Inputs:** Rounded rectangular with soft radius (`border-radius: 10px`).

---

## 7. Component Specifications

### Primary CTA Button (Volt Pulse)
```css
background: #D4FF00;
color: #08090A;
font-family: 'Plus Jakarta Sans', sans-serif;
font-weight: 700;
font-size: 15px;
border-radius: 9999px;
padding: 12px 28px;
border: none;
transition: transform 0.15s ease, background 0.15s ease;
```
*Hover state:* scales to `1.02`, background lightens to `#BCE000`.

### Secondary Outlined Button
```css
background: transparent;
color: #F8FAFC;
font-weight: 600;
border: 1px solid #242A33;
border-radius: 9999px;
padding: 12px 24px;
```
*Hover state:* background becomes `#1A1E24`, border shifts to `#94A3B8`.

### Biometric Match Tag (AI Indicator)
```css
background: rgba(0, 240, 255, 0.1);
color: #00F0FF;
border: 1px solid rgba(0, 240, 255, 0.25);
font-family: 'JetBrains Mono', monospace;
font-size: 11px;
padding: 4px 10px;
border-radius: 9999px;
```

---

## 8. Do's and Don'ts

### DO:
- ✅ **DO** prioritize mobile thumb zones for all interactive triggers (bottom sheets, sticky CTAs).
- ✅ **DO** use real fitness imagery and authentic sports data (bpm, reps, tracks, session names) instead of "Lorem Ipsum" or generic SaaS metrics.
- ✅ **DO** keep background dark and let content, photos, and high-energy volt accents deliver visual excitement.

### DON'T:
- ❌ **DON'T** use multi-color pastel rainbow badges.
- ❌ **DON'T** use low-contrast gray text on dark backgrounds (always maintain WCAG AA minimum 4.5:1).
- ❌ **DON'T** rely on giant floating 3D glass balls or irrelevant tech gradient blobs.
