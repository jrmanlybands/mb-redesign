# Manly Bands Redesign (mb-redesign)

## Project Overview

A complete homepage redesign for **Manly Bands**, a men's wedding bands e-commerce brand. This is a single-file static website (`index.html`) containing all HTML, CSS, and JavaScript — no build tools, no frameworks, no dependencies beyond Google Fonts and Unsplash CDN images.

The design language is inspired by [Knockaround](https://knockaround.com/) — left-justified horizontal scroll sections, bold typography, rounded cards, and a mobile-first swipable UX.

## Architecture

```
mb-redesign/
├── index.html          # Entire site: HTML + CSS + JS (~1600 lines)
├── images/             # Local product images
│   ├── ceo.jpg
│   ├── cowboy.jpg
│   ├── baller.jpg
│   ├── rockstar.jpg
│   ├── boss.jpg
│   └── hero.jpg
├── CLAUDE.md           # This file
└── .claude/
    └── launch.json     # Dev server config (Python HTTP, port 8766)
```

### Single-File Architecture

Everything lives in `index.html`:
- **Lines 1–1071**: `<style>` block (all CSS)
- **Lines 1072–1574**: HTML body (all sections)
- **Lines 1575–1620**: `<script>` block (all JS)

## Design System

### Brand Colors
| Token | Hex | Usage |
|-------|-----|-------|
| Primary Gold | `#c8922a` | CTAs, badges, accents, links on hover, stars |
| Dark | `#1a1a1a` | Text, header, active tabs, footer bg variant |
| Light BG | `#f5f5f5` / `#f7f7f7` | Card backgrounds, section alternation |
| White | `#fff` | Page background, button text |

### Typography
- **Headings**: `Oswald` (weights 400–700), uppercase, tight letter-spacing
- **Body**: `Inter` (weights 400–600), system font fallbacks
- All section titles use `.section-title` — 36px Oswald bold uppercase

### Buttons
- `.btn-primary` — Gold background, white text, 12px rounded corners
- `.btn-outline` — Transparent with gold border
- `.btn-outline-white` — Transparent with white border (used on dark banners)

### Spacing & Layout
- `.container` — `max-width: 1440px; padding: 0 40px; margin: 0 auto`
- Scroll sections override container: `max-width: 100%; padding: 0 0 0 40px` (left-justified, bleeds right)
- Section vertical padding: typically `60px 0`
- Card border-radius: `12px` throughout

## Page Sections (top to bottom)

### 1. Benefits Bar
Black top bar with three trust signals: Lifetime Warranty, Free Silicone, Free Shipping. SVG icons inline.

### 2. Header / Nav
Sticky header with logo (SVG + "Manly Bands"), nav links (hidden on mobile), icon buttons (search, account, cart). Gains shadow on scroll via JS class toggle.

### 3. Promo Banner
Gold (`#c8922a`) banner with sale messaging. Sits below header.

### 4. Hero
Full-width, 620px tall (480px mobile). Unsplash background image with dark overlay. Contains h1, tagline, and two CTAs (primary + outline).

### 5. Shop by Material
- **Desktop**: Horizontal scroll with 120px circle tiles, left-justified container
- **Mobile (≤768px)**: Switches to a **3-column CSS grid** with 120px circles, centered with `margin: 0 auto`, symmetric 20px padding
- **12 materials shown**: Gold, Titanium, Tungsten, Wood, Carbon Fiber, Meteorite, Damascus, Rose Gold, Black Zirconium, Antler, Silicone, Ceramic
- Material colors are CSS gradients (`.mat-gold`, `.mat-titanium`, etc.)

### 6. Build Your Own Band Banner
Full-width dark banner (500px) with Unsplash background, gradient overlay, and CTA.

### 7. Best Sellers
- **Title row**: "BEST SELLERS" heading + carousel prev/next buttons (`.best-sellers-title-row`, `align-items: flex-start`)
- **Filter tabs**: ALL, GOLD, BLACK, TUNGSTEN, TITANIUM (`.tab` buttons with active state)
- **Product grid**: Horizontal flex scroll with snap alignment
- **Desktop**: Cards at 280px wide (260px at ≤1024px)
- **Mobile (≤768px)**: Cards at **250px** wide, 12px gap, 16px left padding — shows ~1 full card + 40% peek of 2nd card (Knockaround pattern)
- **Tabs on mobile**: Shrunk to 11px font, 6px gap, 6px/12px padding to fit all 5 on one line
- **Carousel buttons**: Wired via JS — scrolls by one card width (+ gap) per click, smooth behavior
- **Product cards** include: badge ("30% OFF"), product image, star rating, name + material style, original/sale prices, "+X MORE MATERIALS" link

### 8. Collection Tiles
Horizontal scroll of rounded image cards with gradient overlays and bottom-left labels. 8 tiles: Most Popular, Military Heritage, Jack Daniel's, Lord of the Rings, DC, Fender, Jeep, NASA-Inspired.
- **Desktop**: `min-width: 425px; height: 300px`
- **Tablet (≤1024px)**: `min-width: 280px`
- **Mobile (≤768px)**: `min-width: 385px; height: 290px` — nearly full-width with peek

### 9. Custom Builder Section
Dark (`#1a1a1a`) split-layout: text left, Unsplash image right (55% width). Eyebrow text in gold, large heading, paragraph, and outline-white CTA.

### 10. Licensed / Partnerships
Horizontal scroll of large square cards (425x425px) for licensed collections: Lord of the Rings, Jack Daniel's, DC Comics, Fender, Jeep. Has its own carousel nav buttons.

### 11. What's Your Style?
3-column grid of tall image cards (380px) with style tags ("Historical", "Imaginative", "Rugged"). Collapses to single column on mobile.

### 12. Dare to Be Different Banner
Full-width lifestyle banner (450px) with gradient overlay and CTA.

### 13. Real Rings for Real Men
Two-column grid: image left, text + CTA right. Collapses to single column on mobile.

### 14. Press / Social Proof
Centered quote with press logos (Rolling Stone, WSJ, GQ, Variety, Forbes, Nerdist). Each logo has custom font styling to approximate the real brand look.

### 15. Military Section
Full-width banner with gradient overlay, heading, and CTA for military/first responder discounts.

### 16. Footer
- **Help section**: Centered heading with three action buttons (Track Order, Start a Return, Help Center)
- **Columns**: Info links, Support links, Newsletter signup (email input + submit)
- **Bottom bar**: Copyright + social icons

## Responsive Breakpoints

### ≤1024px (Tablet)
- Material circles: 100px
- Product cards: 260px
- Collection tiles: min-width 280px

### ≤768px (Mobile)
- Container padding: 20px
- Benefits bar: 10px font, 16px gap
- Nav links: hidden
- Hero: 480px height, 38px h1
- **Materials**: Grid 3-col layout, 120px circles, symmetric 20px padding
- **Best Sellers**: 250px cards, 12px gap, 16px left padding, smaller tabs (11px)
- **Collection tiles**: 385px x 290px
- Footer: single column
- Banners: 360px height, 36px h2
- Style grid: single column

## JavaScript Behavior

All JS is in a single `<script>` block at the bottom of the file:

1. **Sticky header shadow**: Adds `.scrolled` class when `scrollY > 10`
2. **Tab switching**: Click handler toggles `.active` class on filter tabs
3. **Best sellers carousel**: Prev/next buttons scroll `.products-grid` by one card width + gap, using `scrollBy()` with `behavior: 'smooth'`
4. **Image fallback**: On `error`, replaces broken `<img>` with a gradient placeholder + alt text label

## Horizontal Scroll Pattern (used throughout)

The Knockaround-inspired scroll pattern is applied to multiple sections:

```css
.scroll-container {
  display: flex;
  gap: [varies];
  overflow-x: auto;
  scroll-snap-type: x mandatory;
  -webkit-overflow-scrolling: touch;
  scrollbar-width: none;            /* Firefox */
}
.scroll-container::-webkit-scrollbar { display: none; }  /* Chrome/Safari */
.scroll-item {
  flex-shrink: 0;
  width: [fixed width];
  scroll-snap-align: start;
}
```

Left-justified containers use: `max-width: 100%; padding: 0 0 0 40px` — no right padding so cards bleed to the viewport edge.

## Dev Server

Configured in `.claude/launch.json`:
```json
{
  "command": "python3 -m http.server 8766",
  "port": 8766
}
```

Run with: `python3 -m http.server 8766` from the project root.

## External Dependencies

- **Google Fonts**: Oswald (400–700) + Inter (400–600)
- **Unsplash**: Hero, Build Your Own, Custom Builder, Dare, Military, Real Rings, Style cards, Collection tiles — all via `images.unsplash.com` CDN URLs
- **Local images**: Product ring photos in `images/` directory (ceo.jpg, cowboy.jpg, baller.jpg, rockstar.jpg, boss.jpg)

## Key Design Decisions

1. **Single file**: Keeps things simple, no build step, easy to deploy anywhere
2. **Left-justified scroll**: Sections bleed to the right edge, signaling swipability
3. **Mobile material grid**: Switches from horizontal scroll to 3-column grid on mobile for easier browsing (12 tiles, 4 rows)
4. **Card peek pattern**: On mobile, product cards are sized so the next card peeks into view (~40% visible), indicating scrollability without explicit UI
5. **Hidden scrollbars**: Native scrollbar hidden on all scroll sections for cleaner aesthetic; scroll-snap provides precise card alignment
6. **CSS-only material swatches**: Material circles use CSS gradients instead of images for faster loading and consistency
