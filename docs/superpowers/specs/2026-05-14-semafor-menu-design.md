# Semafor Caffe — Interactive Online Menu Design Spec
Date: 2026-05-14

## Overview

A single-file interactive HTML/CSS menu for Semafor Caffe, delivered via QR code. No JavaScript, no external dependencies. Works offline from any browser.

## Technology

- **Single file**: `index.html` with all CSS embedded in a `<style>` block
- **Tab switching**: Hidden `<input type="radio">` elements; CSS `:checked ~ .panel` rules show/hide content panels
- **No JavaScript**

## Color Palette

| Token | Hex | Usage |
|---|---|---|
| Background | `#0d1b2a` | Page background |
| Surface | `#112236` | Menu item rows / cards |
| Gold | `#c9a84c` | Category headers, active tab, prices |
| Cream | `#e8dcc8` | Body text |
| Muted | `#7a8fa6` | Inactive tab labels |
| Red | `#e03535` | Traffic light dot (decorative) |
| Amber | `#e8a020` | Traffic light dot (decorative) |
| Green | `#2e9e5b` | Traffic light dot (decorative) |

## Typography

- **Category headers**: `Georgia, 'Times New Roman', serif` — gold color, letter-spaced
- **Item names & prices**: `-apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif` — readable at small sizes
- **Tab labels**: sans-serif, uppercase, small caps feel

## Layout

### Header (fixed, top)
- Centered logo placeholder: 80px circle, gold border, gold dashed inner ring, "LOGO" label in muted text
- "SEMAFOR CAFFE" in gold, spaced caps below logo
- Three traffic-light dots (red · amber · green) as decorative accent below the title
- Background: deep navy, subtle bottom border in gold

### Content Area
- Scrollable, positioned between fixed header and fixed tab bar
- Padding: comfortable mobile spacing (16px sides)
- Each **category** has:
  - Gold serif heading
  - Thin gold horizontal rule beneath
  - Card container for items
- Each **menu item** is a flex row:
  - Name on left (cream)
  - Dotted gold separator line (flex-grow)
  - Price on right (gold)

### Bottom Tab Bar (fixed)
- 5 equal-width tabs spanning full width
- Background: `#0a1520` (darker navy)
- Gold top border on active tab
- Active label: gold; inactive: muted

| # | Label | Icon | Content |
|---|---|---|---|
| 1 | Topli | ☕ | TOPLI NAPICI |
| 2 | Hladne | ❄️ | HLADNE KAFE |
| 3 | Ukusi | ✨ | KAFE SA UKUSOM + DODACI |
| 4 | Sokovi | 🥤 | GAZIRANI + NEGAZIRANI + VODE |
| 5 | Alkohol | 🍸 | ALKOHOLNA PIĆA + CEĐENI SOKOVI |

## Menu Content

### Tab 1 — TOPLI NAPICI
Espreso 180 · Dopio 260 · Espreso sa mlekom 190 · Ristreto 180 · Lungo 180 · Kapućino 210 · Amerikano 180 · Domaća kafa 180 · Flet vajt 300 · Makijato 190 · Kafe late 240 · Espreso sa sojinim mlekom 220 · Čaj 180 · Topla čokolada 300

### Tab 2 — HLADNE KAFE
Fredo 210 · Fredo kapućino 240 · Afogato 300 · Ajс kafa 320 · Hladni Nes 240 · Hladni Nes sa sojinim mlekom 300 · Hladni Late 240

### Tab 3 — KAFE SA UKUSOM + DODACI
**Kafe sa ukusom**: Hejzel ajc late 280 · Karamel ajc late 280 · Vanila ajc late 280 · Ajc moka 280 · Hejzel late 280 · Karamel late 280 · Vanila late 280

**Dodaci**: Šlag 50 · Sojino mleko 50 · Lešnik 60 · Karamela 60 · Vanila 60 · Sladoled 100

### Tab 4 — SOKOVI & VODA
**Gazirani**: Pepsi · Pepsi Zero · Pepsi Tvist · Mirinda · 7up · Everves tonik · Everves Biter Lemon · Klaker Crveni Kruška (sve 210) · Oranžina 280

**Negazirani**: Kjub Jabuka · Kjub Narandža · Kjub Jagoda · Kjub Breskva · Kjub Ananas · Kjub Borovnica (sve 220)

**Vode**: Knjaz Miloš 180 · Akva Viva 180 · Knjaz Limun 240 · Knjaz Mandarina 240 · Guarana 220

### Tab 5 — ALKOHOL & CEĐENI SOKOVI
**Alkoholna pića**: Niško pivo 180 · Džejmison 320 · Gorki list 220 · Rubin Pelinkovac 220 · Zekić 220 · Vodka 250 · Džin Gordons 280 · Bejlis 220 · Belo vino Rubin Tamjanika 470 · Crno vino Rubin Kabernet Sovinjon 470 · Somerzbi Mango 320 · Somerzbi Kruška 320 · Somerzbi Borovnica 320

**Ceđeni sokovi**: Ceđeni sok Narandža 260 · Ceđeni sok Limun 240 · Ceđeni miks 280 · Stroberi sanset 320 · Pič sanset 320 · Razberi sanset 320 · Pajnapl sanset 320

## Responsive Behavior

- Designed mobile-first (375px–430px primary target)
- Header logo scales down on very small screens
- Tab labels truncate gracefully; icons always visible
- Font sizes use `clamp()` or fixed small values that work at 375px

## Delivery

- Single `index.html` file in repo root
- QR code points to hosted URL (GitHub Pages / Netlify recommended) or directly to the file
