# Semafor Caffe — Digital Menu

QR-code drink menu for [Semafor Caffe](https://caffesemafor.com), a café in Serbia. Guests scan a QR code at the table and get a fast, mobile-first menu with six categories: hot drinks, iced coffees, flavored coffees, soft drinks, alcohol, and fresh-squeezed juices.

**Live:** [caffesemafor.com](https://caffesemafor.com)

## Why a single HTML file

This is a deliberate engineering choice, not a shortcut. The site is one page of static content viewed almost exclusively on phones over cellular connections:

- **Zero dependencies, zero build step** — nothing to install, update, or break. The whole site is one `index.html`.
- **Fast on cellular** — hero photos are compressed WebP (~300 KB total for six full-screen images), lazy-loaded below the fold.
- **No framework overhead** — a menu doesn't need hydration, routing, or state management. Vanilla JS handles the two behaviors that exist: smooth-scroll tab navigation and a scroll spy.

## Implementation notes

- **Layout** — fixed header and bottom tab bar with a scrollable panel between them; each section has a sticky full-viewport hero photo that the menu content scrolls over. Uses `dvh` units and `env(safe-area-inset-bottom)` for correct rendering around iOS Safari's toolbars and the home indicator.
- **Navigation** — bottom tab bar (native-app pattern) with inline SVG icons; a scroll spy keeps the active tab (and `aria-current`) in sync while scrolling.
- **Animation** — `IntersectionObserver`-driven entrance animations with staggered delays; Ken Burns effect on hero photos. All motion is disabled under `prefers-reduced-motion`.
- **Semantics & accessibility** — landmark structure (`header`/`main`/`nav`/`footer`), menu items as lists, labeled sections, real `<button>` elements for tabs, `lang="sr"`.

## Deployment

Served by GitHub Pages with a custom domain (see `CNAME`). Every push to `main` deploys.

## Credits

Designed & built by [Webmasters Pro](https://www.webmasters-pro.com/sr) for Semafor Caffe.
