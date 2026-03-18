# Manly Bands Redesign (mb-redesign)

## Project Overview

A complete homepage redesign for **Manly Bands**, a men's wedding bands e-commerce brand. This is a single-file static website (`index.html`) containing all HTML, CSS, and JavaScript — no build tools, no frameworks, no dependencies beyond Google Fonts, Shopify CDN product images, and Unsplash CDN lifestyle images.

The design language is inspired by [Knockaround](https://knockaround.com/) — left-justified horizontal scroll sections, bold typography, rounded cards, and a mobile-first swipable UX.

## Architecture

```
mb-redesign/
├── index.html          # Entire site: HTML + CSS + JS (~1700 lines)
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
- **`<style>` block**: All CSS (~1070 lines)
- **HTML body**: All sections
- **`<script>` block**: All JS (tab filtering, carousel, header scroll, image fallback)

## Design System

### Brand Colors
| Token | Hex | Usage |
|-------|-----|-------|
| Primary Gold | `#c8922a` | CTAs, badges, accents, links on hover, stars |
| Dark | `#1a1a1a` | Text, header, active tabs, footer bg variant |
| Light BG | `#f5f5f5` / `#f7f7f7` | Card backgrounds, section alternation |
| White | `#fff` | Page background, button text, material image backgrounds |

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
Sticky header with official Manly Bands SVG logo (inlined from `manlybands.com/svgs/logo.svg`, 61px height), nav links (hidden on mobile), icon buttons (search, account, cart). Gains shadow on scroll via JS class toggle.

### 3. Promo Banner
Gold (`#c8922a`) banner with sale messaging. Sits below header.

### 4. Hero
Full-width, 620px tall (480px mobile). Unsplash background image with dark overlay. Contains h1, tagline, and two CTAs (primary + outline).

### 5. Shop by Material
- **Desktop**: Wrapping flex grid (`flex-wrap: wrap`) with 200px-wide items, left-justified. No horizontal scroll — flows into two rows (typically 7 + 5 or 6 + 6 depending on viewport)
- **Mobile (≤768px)**: Switches to a **3-column CSS grid** with full-width images, symmetric 20px padding
- **12 materials shown**: Gold, Titanium, Tungsten, Wood, Carbon Fiber, Meteorite, Damascus, Rose Gold, Black Zirconium, Antler, Silicone, Ceramic
- **Product images**: Real ring photos from Shopify CDN (white backgrounds, `object-fit: contain`)
- **Material labels**: 16px Oswald uppercase on both desktop and mobile

### 6. Build Your Own Band Banner
Full-width dark banner (500px) with Unsplash background, gradient overlay, and CTA.

### 7. Best Sellers
- **Title row**: "BEST SELLERS" heading + carousel prev/next buttons (`.best-sellers-title-row`, `align-items: center`), carousel buttons offset `top: -15px`
- **Filter tabs**: ALL, GOLD, BLACK, TUNGSTEN, TITANIUM (`.tab` buttons with active state)
- **Tab filtering**: JS filters product cards by `data-category` attribute; clicking a tab shows only matching cards and resets scroll position
- **Product grid**: Horizontal flex scroll with snap alignment
- **Desktop**: Cards at 280px wide (260px at ≤1024px)
- **Mobile (≤768px)**: Cards at **250px** wide, 12px gap, 16px left padding
- **Tabs on mobile**: Shrunk to 11px font, 6px gap, 6px/12px padding
- **Carousel buttons**: Scrolls by one card width (+ gap) per click, smooth behavior
- **Product cards**: badge ("30% OFF"), product image (Shopify CDN), star rating, name + material style, original/sale prices, "+X MORE MATERIALS" link. Hover zooms image only (no card lift)
- **Product categories**: Gold (CEO, MVP), Black (Baller, Genius, Ash), Tungsten (Cowboy, Guide), Titanium (Gandalf, Sage, Oryx)

### 8. Popular Collections
Horizontal scroll of rounded image cards with gradient overlays and bottom-left labels. Section title: "POPULAR COLLECTIONS". 8 tiles: Most Popular, Military Heritage, Jack Daniel's, Lord of the Rings, DC, Fender, Jeep, NASA-Inspired.
- **Desktop**: `min-width: 425px; height: 300px`
- **Tablet (≤1024px)**: `min-width: 280px`
- **Mobile (≤768px)**: `min-width: 308px; height: 232px` (20% smaller)

### 9. Custom Builder Section
Dark (`#1a1a1a`) split-layout: text left, Unsplash image right (55% width). Eyebrow text in gold, large heading, paragraph, and outline-white CTA.

### 10. Officially Licensed Collections
Horizontal scroll of square cards (340x340px) for licensed collections: Lord of the Rings, Jack Daniel's, DC Comics, Fender, Jeep. Section title: "OFFICIALLY LICENSED COLLECTIONS". Has its own carousel nav buttons.

### 11. Dare to Be Different Banner
Full-width lifestyle banner (450px) with gradient overlay and CTA.

### 12. Real Rings for Real Men
Two-column grid: image left, text + CTA right. Collapses to single column on mobile.

### 13. Press / Social Proof
Centered quote with press logos (Rolling Stone, WSJ, GQ, Variety, Forbes, Nerdist). Each logo has custom font styling to approximate the real brand look.

### 14. Military Section
Full-width banner with gradient overlay, heading, and CTA for military/first responder discounts.

### 15. Footer
- **Help section**: Centered heading with three action buttons (Track Order, Start a Return, Help Center)
- **Columns**: Info links, Support links, Newsletter signup (email input + submit)
- **Bottom bar**: Copyright + social icons

## Responsive Breakpoints

### ≤1024px (Tablet)
- Material items: 100px (via tablet override)
- Product cards: 260px
- Collection tiles: min-width 280px

### ≤768px (Mobile)
- Container padding: 20px
- Benefits bar: 10px font, 16px gap
- Nav links: hidden
- Hero: 480px height, 38px h1
- **Materials**: Grid 3-col layout, full-width images, 16px labels
- **Best Sellers**: 250px cards, 12px gap, 16px left padding, smaller tabs (11px)
- **Collection tiles**: 308px x 232px (20% smaller than desktop)
- Footer: single column
- Banners: 360px height, 36px h2

## JavaScript Behavior

All JS is in a single `<script>` block at the bottom of the file:

1. **Sticky header shadow**: Adds `.scrolled` class when `scrollY > 10`
2. **Tab filtering**: Click handler toggles `.active` class and filters `.product-card` elements by `data-category` attribute. "All" shows everything; other tabs show only matching cards. Resets scroll position on filter change.
3. **Best sellers carousel**: Prev/next buttons scroll `.products-grid` by one card width + gap, using `scrollBy()` with `behavior: 'smooth'`
4. **Image fallback**: On `error`, replaces broken `<img>` with a gradient placeholder + alt text label

## Horizontal Scroll Pattern (used throughout)

The Knockaround-inspired scroll pattern is applied to Collection Tiles, Licensed Collections, and Best Sellers:

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

**Note**: Shop by Material no longer uses horizontal scroll on desktop — it uses `flex-wrap: wrap` to flow into multiple rows.

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
- **Shopify CDN**: Product ring images for Shop by Material and Best Sellers sections (via `cdn.shopify.com`)
- **Unsplash**: Hero, Build Your Own, Custom Builder, Dare, Military, Real Rings, Collection tiles, Licensed collections — all via `images.unsplash.com` CDN URLs
- **Manly Bands logo**: Inlined SVG sourced from `manlybands.com/svgs/logo.svg`
- **Local images**: Product ring photos in `images/` directory (ceo.jpg, cowboy.jpg, baller.jpg, rockstar.jpg, boss.jpg)

## Key Design Decisions

1. **Single file**: Keeps things simple, no build step, easy to deploy anywhere
2. **Left-justified scroll**: Sections bleed to the right edge, signaling swipability
3. **Desktop material grid**: Uses `flex-wrap` instead of horizontal scroll so all 12 materials are visible without scrolling (two rows)
4. **Mobile material grid**: Switches to 3-column CSS grid with full-width images for easier browsing
5. **Card peek pattern**: On mobile, product cards and collection tiles are sized so the next card peeks into view, indicating scrollability without explicit UI
6. **Hidden scrollbars**: Native scrollbar hidden on all scroll sections for cleaner aesthetic; scroll-snap provides precise card alignment
7. **Real product images**: Material swatches use actual Shopify CDN ring photos on white backgrounds instead of CSS gradients
8. **Tab filtering**: Best Sellers tabs actively filter products by category using `data-category` attributes, not just visual state
9. **Image-only hover**: Product cards zoom the image on hover without lifting the card, keeping the badge stationary
