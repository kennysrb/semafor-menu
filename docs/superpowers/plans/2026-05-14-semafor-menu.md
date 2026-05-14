# Semafor Caffe Interactive Menu — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a single `index.html` file with embedded CSS that serves as a 5-tab interactive QR-code-accessible menu for Semafor Caffe, with no JavaScript or external dependencies.

**Architecture:** Hidden `<input type="radio">` elements at the top of `<body>` control tab panel visibility via CSS `:checked ~ sibling` selectors. Fixed header (logo + title), scrollable content panels, fixed bottom tab bar. All styles embedded in `<style>` block.

**Tech Stack:** HTML5, CSS3 (custom properties, flexbox, `:checked` selector, `env()` safe-area-inset)

---

## File Structure

| File | Responsibility |
|---|---|
| `index.html` | Everything — markup, embedded CSS, all content |

---

### Task 1: HTML Skeleton + CSS Foundation

**Files:**
- Create: `index.html`

- [ ] **Step 1: Create `index.html` with boilerplate, CSS custom properties, and reset**

```html
<!DOCTYPE html>
<html lang="sr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
  <title>Semafor Caffe</title>
  <style>
    :root {
      --bg:       #0d1b2a;
      --surface:  #112236;
      --gold:     #c9a84c;
      --cream:    #e8dcc8;
      --muted:    #7a8fa6;
      --tab-bg:   #0a1520;
      --red:      #e03535;
      --amber:    #e8a020;
      --green:    #2e9e5b;
      --header-h: 110px;
      --tabbar-h: 64px;
    }

    *, *::before, *::after {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    html, body {
      height: 100%;
      overflow: hidden;
    }

    body {
      background: var(--bg);
      color: var(--cream);
      font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
      font-size: 15px;
    }
  </style>
</head>
<body>
</body>
</html>
```

- [ ] **Step 2: Open `index.html` in a browser**

Expected: Dark navy (`#0d1b2a`) full-screen page with no content.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add HTML skeleton and CSS foundation"
```

---

### Task 2: Radio Inputs + Tab Switching CSS

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add 5 hidden radio inputs as first children of `<body>`**

Add inside `<body>`, before everything else:

```html
  <!-- Tab state controllers — must be first in body for ~ sibling selectors -->
  <input type="radio" name="tab" id="tab1" checked>
  <input type="radio" name="tab" id="tab2">
  <input type="radio" name="tab" id="tab3">
  <input type="radio" name="tab" id="tab4">
  <input type="radio" name="tab" id="tab5">
```

- [ ] **Step 2: Add 5 panels inside `<main class="panels">` after the radio inputs**

```html
  <main class="panels">
    <div class="panel" id="panel1"><p style="color:white">Panel 1</p></div>
    <div class="panel" id="panel2"><p style="color:white">Panel 2</p></div>
    <div class="panel" id="panel3"><p style="color:white">Panel 3</p></div>
    <div class="panel" id="panel4"><p style="color:white">Panel 4</p></div>
    <div class="panel" id="panel5"><p style="color:white">Panel 5</p></div>
  </main>
```

- [ ] **Step 3: Add tab switching CSS to the `<style>` block**

```css
    input[name="tab"] { display: none; }

    .panels {
      position: fixed;
      top: var(--header-h);
      bottom: var(--tabbar-h);
      left: 0;
      right: 0;
      overflow-y: auto;
      -webkit-overflow-scrolling: touch;
      scrollbar-width: none;
    }
    .panels::-webkit-scrollbar { display: none; }

    .panel { display: none; padding: 20px 16px 24px; }

    #tab1:checked ~ .panels #panel1 { display: block; }
    #tab2:checked ~ .panels #panel2 { display: block; }
    #tab3:checked ~ .panels #panel3 { display: block; }
    #tab4:checked ~ .panels #panel4 { display: block; }
    #tab5:checked ~ .panels #panel5 { display: block; }
```

- [ ] **Step 4: Verify in browser**

Open `index.html`. Only "Panel 1" text should be visible (panel1 is shown because tab1 is `checked` by default). No other panel text visible.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: add radio tab switching mechanism"
```

---

### Task 3: Header

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add header HTML between radio inputs and `<main>`**

```html
  <header class="header">
    <div class="logo-placeholder">LOGO</div>
    <h1 class="cafe-title">SEMAFOR CAFFE</h1>
    <div class="traffic-lights">
      <span class="dot dot-red"></span>
      <span class="dot dot-amber"></span>
      <span class="dot dot-green"></span>
    </div>
  </header>
```

- [ ] **Step 2: Add header CSS to the `<style>` block**

```css
    .header {
      position: fixed;
      top: 0; left: 0; right: 0;
      height: var(--header-h);
      background: var(--bg);
      border-bottom: 1px solid rgba(201, 168, 76, 0.3);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 8px 0 6px;
      z-index: 100;
    }

    .logo-placeholder {
      width: 64px;
      height: 64px;
      border-radius: 50%;
      border: 2px solid var(--gold);
      outline: 2px dashed rgba(201, 168, 76, 0.35);
      outline-offset: -6px;
      display: flex;
      align-items: center;
      justify-content: center;
      color: var(--muted);
      font-size: 10px;
      letter-spacing: 0.1em;
    }

    .cafe-title {
      font-family: Georgia, 'Times New Roman', serif;
      font-size: 13px;
      font-weight: normal;
      letter-spacing: 0.3em;
      color: var(--gold);
      margin-top: 5px;
    }

    .traffic-lights {
      display: flex;
      gap: 5px;
      margin-top: 5px;
    }

    .dot {
      width: 7px;
      height: 7px;
      border-radius: 50%;
    }
    .dot-red   { background: var(--red); }
    .dot-amber { background: var(--amber); }
    .dot-green { background: var(--green); }
```

- [ ] **Step 3: Verify in browser**

Expected: Fixed header with centered logo circle (gold border, dashed inner ring, "LOGO" label), "SEMAFOR CAFFE" in gold serif below it, three colored dots (red/amber/green) below title. Panel 1 content should still be visible below the header.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add header with logo placeholder and traffic light accent"
```

---

### Task 4: Bottom Tab Bar

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add tab bar HTML after `</main>`**

```html
  <nav class="tab-bar">
    <label for="tab1" class="tab-label">
      <span class="tab-icon">☕</span>
      <span class="tab-text">Topli</span>
    </label>
    <label for="tab2" class="tab-label">
      <span class="tab-icon">❄️</span>
      <span class="tab-text">Hladne</span>
    </label>
    <label for="tab3" class="tab-label">
      <span class="tab-icon">✨</span>
      <span class="tab-text">Ukusi</span>
    </label>
    <label for="tab4" class="tab-label">
      <span class="tab-icon">🥤</span>
      <span class="tab-text">Sokovi</span>
    </label>
    <label for="tab5" class="tab-label">
      <span class="tab-icon">🍸</span>
      <span class="tab-text">Alkohol</span>
    </label>
  </nav>
```

- [ ] **Step 2: Add tab bar CSS to the `<style>` block**

```css
    .tab-bar {
      position: fixed;
      bottom: 0; left: 0; right: 0;
      height: var(--tabbar-h);
      background: var(--tab-bg);
      border-top: 1px solid rgba(201, 168, 76, 0.15);
      display: flex;
      padding-bottom: env(safe-area-inset-bottom, 0);
      z-index: 100;
    }

    .tab-label {
      flex: 1;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      gap: 2px;
      cursor: pointer;
      border-top: 2px solid transparent;
      -webkit-tap-highlight-color: transparent;
    }

    .tab-icon { font-size: 18px; line-height: 1; }

    .tab-text {
      font-size: 10px;
      letter-spacing: 0.06em;
      text-transform: uppercase;
      color: var(--muted);
    }

    /* Active tab: gold top border + gold label */
    #tab1:checked ~ .tab-bar label[for="tab1"],
    #tab2:checked ~ .tab-bar label[for="tab2"],
    #tab3:checked ~ .tab-bar label[for="tab3"],
    #tab4:checked ~ .tab-bar label[for="tab4"],
    #tab5:checked ~ .tab-bar label[for="tab5"] {
      border-top-color: var(--gold);
    }

    #tab1:checked ~ .tab-bar label[for="tab1"] .tab-text,
    #tab2:checked ~ .tab-bar label[for="tab2"] .tab-text,
    #tab3:checked ~ .tab-bar label[for="tab3"] .tab-text,
    #tab4:checked ~ .tab-bar label[for="tab4"] .tab-text,
    #tab5:checked ~ .tab-bar label[for="tab5"] .tab-text {
      color: var(--gold);
    }
```

- [ ] **Step 3: Verify in browser**

Expected: 5 tabs fixed at bottom. "Topli" tab is active (gold top border, gold label text). Tapping/clicking each tab switches the visible panel. All tabs show correct icons and labels.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add bottom tab bar with active state CSS"
```

---

### Task 5: Category & Item CSS + Tab 1 Content (TOPLI NAPICI)

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add category and item CSS to the `<style>` block**

```css
    .category { margin-bottom: 28px; }

    .category-title {
      font-family: Georgia, 'Times New Roman', serif;
      font-size: 12px;
      font-weight: normal;
      letter-spacing: 0.22em;
      color: var(--gold);
      text-transform: uppercase;
      padding-bottom: 8px;
      border-bottom: 1px solid rgba(201, 168, 76, 0.45);
      margin-bottom: 2px;
    }

    .item {
      display: flex;
      align-items: baseline;
      padding: 9px 0;
      border-bottom: 1px solid rgba(255, 255, 255, 0.04);
    }

    .item-name {
      color: var(--cream);
      font-size: 14px;
      flex-shrink: 0;
    }

    .item-dots {
      flex: 1;
      border-bottom: 1px dotted rgba(201, 168, 76, 0.3);
      margin: 0 10px 3px;
      min-width: 12px;
    }

    .item-price {
      color: var(--gold);
      font-size: 14px;
      font-weight: 500;
      flex-shrink: 0;
    }
```

- [ ] **Step 2: Replace panel1 placeholder with TOPLI NAPICI content**

Replace the `<div class="panel" id="panel1">` content:

```html
    <div class="panel" id="panel1">
      <section class="category">
        <h2 class="category-title">Topli napici</h2>
        <div class="item"><span class="item-name">Espreso</span><span class="item-dots"></span><span class="item-price">180 rsd</span></div>
        <div class="item"><span class="item-name">Dopio</span><span class="item-dots"></span><span class="item-price">260 rsd</span></div>
        <div class="item"><span class="item-name">Espreso sa mlekom</span><span class="item-dots"></span><span class="item-price">190 rsd</span></div>
        <div class="item"><span class="item-name">Ristreto</span><span class="item-dots"></span><span class="item-price">180 rsd</span></div>
        <div class="item"><span class="item-name">Lungo</span><span class="item-dots"></span><span class="item-price">180 rsd</span></div>
        <div class="item"><span class="item-name">Kapućino</span><span class="item-dots"></span><span class="item-price">210 rsd</span></div>
        <div class="item"><span class="item-name">Amerikano</span><span class="item-dots"></span><span class="item-price">180 rsd</span></div>
        <div class="item"><span class="item-name">Domaća kafa</span><span class="item-dots"></span><span class="item-price">180 rsd</span></div>
        <div class="item"><span class="item-name">Flet vajt</span><span class="item-dots"></span><span class="item-price">300 rsd</span></div>
        <div class="item"><span class="item-name">Makijato</span><span class="item-dots"></span><span class="item-price">190 rsd</span></div>
        <div class="item"><span class="item-name">Kafe late</span><span class="item-dots"></span><span class="item-price">240 rsd</span></div>
        <div class="item"><span class="item-name">Espreso sa sojinim mlekom</span><span class="item-dots"></span><span class="item-price">220 rsd</span></div>
        <div class="item"><span class="item-name">Čaj</span><span class="item-dots"></span><span class="item-price">180 rsd</span></div>
        <div class="item"><span class="item-name">Topla čokolada</span><span class="item-dots"></span><span class="item-price">300 rsd</span></div>
      </section>
    </div>
```

- [ ] **Step 3: Verify in browser**

Expected: "Topli" tab active. Gold "TOPLI NAPICI" heading with gold underline rule. 14 menu items in cream text, gold dotted separator, gold price on right. Items scroll vertically if they overflow.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add item styles and Tab 1 TOPLI NAPICI content"
```

---

### Task 6: Tab 2 Content (HLADNE KAFE)

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Replace panel2 placeholder with HLADNE KAFE content**

```html
    <div class="panel" id="panel2">
      <section class="category">
        <h2 class="category-title">Hladne kafe</h2>
        <div class="item"><span class="item-name">Fredo</span><span class="item-dots"></span><span class="item-price">210 rsd</span></div>
        <div class="item"><span class="item-name">Fredo kapućino</span><span class="item-dots"></span><span class="item-price">240 rsd</span></div>
        <div class="item"><span class="item-name">Afogato</span><span class="item-dots"></span><span class="item-price">300 rsd</span></div>
        <div class="item"><span class="item-name">Ajs kafa</span><span class="item-dots"></span><span class="item-price">320 rsd</span></div>
        <div class="item"><span class="item-name">Hladni Nes</span><span class="item-dots"></span><span class="item-price">240 rsd</span></div>
        <div class="item"><span class="item-name">Hladni Nes sa sojinim mlekom</span><span class="item-dots"></span><span class="item-price">300 rsd</span></div>
        <div class="item"><span class="item-name">Hladni Late</span><span class="item-dots"></span><span class="item-price">240 rsd</span></div>
      </section>
    </div>
```

- [ ] **Step 2: Verify in browser**

Tap the "Hladne" tab. Expected: Panel switches, 7 items visible with correct prices.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add Tab 2 HLADNE KAFE content"
```

---

### Task 7: Tab 3 Content (KAFE SA UKUSOM + DODACI)

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Replace panel3 placeholder**

```html
    <div class="panel" id="panel3">
      <section class="category">
        <h2 class="category-title">Kafe sa ukusom</h2>
        <div class="item"><span class="item-name">Hejzel ajs late</span><span class="item-dots"></span><span class="item-price">280 rsd</span></div>
        <div class="item"><span class="item-name">Karamel ajs late</span><span class="item-dots"></span><span class="item-price">280 rsd</span></div>
        <div class="item"><span class="item-name">Vanila ajs late</span><span class="item-dots"></span><span class="item-price">280 rsd</span></div>
        <div class="item"><span class="item-name">Ajs moka</span><span class="item-dots"></span><span class="item-price">280 rsd</span></div>
        <div class="item"><span class="item-name">Hejzel late</span><span class="item-dots"></span><span class="item-price">280 rsd</span></div>
        <div class="item"><span class="item-name">Karamel late</span><span class="item-dots"></span><span class="item-price">280 rsd</span></div>
        <div class="item"><span class="item-name">Vanila late</span><span class="item-dots"></span><span class="item-price">280 rsd</span></div>
      </section>
      <section class="category">
        <h2 class="category-title">Dodaci</h2>
        <div class="item"><span class="item-name">Šlag (10 g)</span><span class="item-dots"></span><span class="item-price">50 rsd</span></div>
        <div class="item"><span class="item-name">Sojino mleko (0,5 dl)</span><span class="item-dots"></span><span class="item-price">50 rsd</span></div>
        <div class="item"><span class="item-name">Lešnik (0,2 dl)</span><span class="item-dots"></span><span class="item-price">60 rsd</span></div>
        <div class="item"><span class="item-name">Karamela (0,2 dl)</span><span class="item-dots"></span><span class="item-price">60 rsd</span></div>
        <div class="item"><span class="item-name">Vanila (0,2 dl)</span><span class="item-dots"></span><span class="item-price">60 rsd</span></div>
        <div class="item"><span class="item-name">Sladoled (50 g)</span><span class="item-dots"></span><span class="item-price">100 rsd</span></div>
      </section>
    </div>
```

- [ ] **Step 2: Verify in browser**

Tap "Ukusi" tab. Expected: Two category sections — "KAFE SA UKUSOM" with 7 items, "DODACI" with 6 items. Both headings in gold, items scroll if needed.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add Tab 3 KAFE SA UKUSOM and DODACI content"
```

---

### Task 8: Tab 4 Content (SOKOVI & VODA)

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Replace panel4 placeholder**

```html
    <div class="panel" id="panel4">
      <section class="category">
        <h2 class="category-title">Gazirani sokovi</h2>
        <div class="item"><span class="item-name">Pepsi (0,25 l)</span><span class="item-dots"></span><span class="item-price">210 rsd</span></div>
        <div class="item"><span class="item-name">Pepsi Zero (0,25 l)</span><span class="item-dots"></span><span class="item-price">210 rsd</span></div>
        <div class="item"><span class="item-name">Pepsi Tvist (0,25 l)</span><span class="item-dots"></span><span class="item-price">210 rsd</span></div>
        <div class="item"><span class="item-name">Mirinda (0,25 l)</span><span class="item-dots"></span><span class="item-price">210 rsd</span></div>
        <div class="item"><span class="item-name">7up (0,25 l)</span><span class="item-dots"></span><span class="item-price">210 rsd</span></div>
        <div class="item"><span class="item-name">Everves tonik (0,25 l)</span><span class="item-dots"></span><span class="item-price">210 rsd</span></div>
        <div class="item"><span class="item-name">Everves Biter Lemon (0,25 l)</span><span class="item-dots"></span><span class="item-price">210 rsd</span></div>
        <div class="item"><span class="item-name">Klaker Crveni Kruška (0,25 l)</span><span class="item-dots"></span><span class="item-price">210 rsd</span></div>
        <div class="item"><span class="item-name">Oranžina (0,25 l)</span><span class="item-dots"></span><span class="item-price">280 rsd</span></div>
      </section>
      <section class="category">
        <h2 class="category-title">Negazirani sokovi</h2>
        <div class="item"><span class="item-name">Kjub Jabuka (0,2 l)</span><span class="item-dots"></span><span class="item-price">220 rsd</span></div>
        <div class="item"><span class="item-name">Kjub Narandža (0,2 l)</span><span class="item-dots"></span><span class="item-price">220 rsd</span></div>
        <div class="item"><span class="item-name">Kjub Jagoda (0,2 l)</span><span class="item-dots"></span><span class="item-price">220 rsd</span></div>
        <div class="item"><span class="item-name">Kjub Breskva (0,2 l)</span><span class="item-dots"></span><span class="item-price">220 rsd</span></div>
        <div class="item"><span class="item-name">Kjub Ananas (0,2 l)</span><span class="item-dots"></span><span class="item-price">220 rsd</span></div>
        <div class="item"><span class="item-name">Kjub Borovnica (0,2 l)</span><span class="item-dots"></span><span class="item-price">220 rsd</span></div>
      </section>
      <section class="category">
        <h2 class="category-title">Vode</h2>
        <div class="item"><span class="item-name">Knjaz Miloš (0,25 l)</span><span class="item-dots"></span><span class="item-price">180 rsd</span></div>
        <div class="item"><span class="item-name">Akva Viva (0,25 l)</span><span class="item-dots"></span><span class="item-price">180 rsd</span></div>
        <div class="item"><span class="item-name">Knjaz Limun (0,33 l)</span><span class="item-dots"></span><span class="item-price">240 rsd</span></div>
        <div class="item"><span class="item-name">Knjaz Mandarina (0,33 l)</span><span class="item-dots"></span><span class="item-price">240 rsd</span></div>
        <div class="item"><span class="item-name">Guarana (0,25 l)</span><span class="item-dots"></span><span class="item-price">220 rsd</span></div>
      </section>
    </div>
```

- [ ] **Step 2: Verify in browser**

Tap "Sokovi" tab. Expected: Three category sections — "GAZIRANI SOKOVI" (9 items), "NEGAZIRANI SOKOVI" (6 items), "VODE" (5 items). Scroll works through all items.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add Tab 4 SOKOVI and VODE content"
```

---

### Task 9: Tab 5 Content (ALKOHOL & CEĐENI SOKOVI)

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Replace panel5 placeholder**

```html
    <div class="panel" id="panel5">
      <section class="category">
        <h2 class="category-title">Alkoholna pića</h2>
        <div class="item"><span class="item-name">Niško pivo (0,33 l)</span><span class="item-dots"></span><span class="item-price">180 rsd</span></div>
        <div class="item"><span class="item-name">Džejmison (0,03 l)</span><span class="item-dots"></span><span class="item-price">320 rsd</span></div>
        <div class="item"><span class="item-name">Gorki list (0,03 l)</span><span class="item-dots"></span><span class="item-price">220 rsd</span></div>
        <div class="item"><span class="item-name">Rubin Pelinkovac (0,03 l)</span><span class="item-dots"></span><span class="item-price">220 rsd</span></div>
        <div class="item"><span class="item-name">Zekić (0,03 l)</span><span class="item-dots"></span><span class="item-price">220 rsd</span></div>
        <div class="item"><span class="item-name">Vodka (0,03 l)</span><span class="item-dots"></span><span class="item-price">250 rsd</span></div>
        <div class="item"><span class="item-name">Džin Gordons (0,03 l)</span><span class="item-dots"></span><span class="item-price">280 rsd</span></div>
        <div class="item"><span class="item-name">Bejlis (0,03 l)</span><span class="item-dots"></span><span class="item-price">220 rsd</span></div>
        <div class="item"><span class="item-name">Belo vino – Rubin Tamjanika (0,187 l)</span><span class="item-dots"></span><span class="item-price">470 rsd</span></div>
        <div class="item"><span class="item-name">Crno vino – Rubin Kabernet Sovinjon (0,187 l)</span><span class="item-dots"></span><span class="item-price">470 rsd</span></div>
        <div class="item"><span class="item-name">Somerzbi – Mango (0,33 l)</span><span class="item-dots"></span><span class="item-price">320 rsd</span></div>
        <div class="item"><span class="item-name">Somerzbi – Kruška (0,33 l)</span><span class="item-dots"></span><span class="item-price">320 rsd</span></div>
        <div class="item"><span class="item-name">Somerzbi – Borovnica (0,33 l)</span><span class="item-dots"></span><span class="item-price">320 rsd</span></div>
      </section>
      <section class="category">
        <h2 class="category-title">Ceđeni sokovi</h2>
        <div class="item"><span class="item-name">Ceđeni sok – Narandža (0,2 l)</span><span class="item-dots"></span><span class="item-price">260 rsd</span></div>
        <div class="item"><span class="item-name">Ceđeni sok – Limun (0,2 l)</span><span class="item-dots"></span><span class="item-price">240 rsd</span></div>
        <div class="item"><span class="item-name">Ceđeni miks (0,2 l)</span><span class="item-dots"></span><span class="item-price">280 rsd</span></div>
        <div class="item"><span class="item-name">Stroberi sanset (0,2 l)</span><span class="item-dots"></span><span class="item-price">320 rsd</span></div>
        <div class="item"><span class="item-name">Pič sanset (0,2 l)</span><span class="item-dots"></span><span class="item-price">320 rsd</span></div>
        <div class="item"><span class="item-name">Razberi sanset (0,2 l)</span><span class="item-dots"></span><span class="item-price">320 rsd</span></div>
        <div class="item"><span class="item-name">Pajnapl sanset (0,2 l)</span><span class="item-dots"></span><span class="item-price">320 rsd</span></div>
      </section>
    </div>
```

- [ ] **Step 2: Verify in browser**

Tap "Alkohol" tab. Expected: Two sections — "ALKOHOLNA PIĆA" (13 items) and "CEĐENI SOKOVI" (7 items). Scroll works through all content.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add Tab 5 ALKOHOL and CEDJENI SOKOVI content"
```

---

### Task 10: Final Polish

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add item hover/tap feedback CSS**

```css
    .tab-label:active { opacity: 0.7; }

    .item:last-child { border-bottom: none; }
```

- [ ] **Step 2: Add a smooth panel scroll-to-top on tab switch**

Because CSS cannot scroll the panel to the top when switching tabs, add this workaround: each panel starts at scroll position 0 by nature of `display: none` toggling. Confirm this works by scrolling down in a tab, switching away, and switching back — the panel should be back at the top.

Expected: Each tab switch resets to top of that tab's content. (This is automatic with `display: none/block` — no code needed. Just verify.)

- [ ] **Step 3: Test on mobile viewport in browser devtools**

Open browser DevTools → Toggle device toolbar → Set to iPhone 14 (390×844). Verify:
- Header is fully visible and not clipped
- Tab bar is above home indicator (iOS safe area respected via `env(safe-area-inset-bottom)`)
- Content area scrolls smoothly
- All 5 tabs switch correctly
- Text is readable without zooming

- [ ] **Step 4: Final commit**

```bash
git add index.html
git commit -m "feat: add tap feedback polish and verify mobile layout"
```

---

## Completion Checklist

- [ ] All 5 tabs switch correctly
- [ ] All menu content matches the spec (Serbian text, correct prices)
- [ ] Header shows logo placeholder + title + traffic light dots
- [ ] Active tab has gold top border and gold label
- [ ] Content scrolls within the panel area (not full page)
- [ ] Works without any JavaScript
- [ ] Works offline (open as local file)
- [ ] Looks correct on 375px wide viewport
