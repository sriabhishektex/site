# CLAUDE.md — AI Assistant Guide for Sri Abhishek Tex Website

## Project Overview

Static marketing website for **Sri Abhishek Tex**, a premium industrial oil distribution company. Pure HTML/CSS/JS with zero build tooling or framework dependencies.

## File Structure

```
/
├── index.html      # Home page (hero, product cards, feature banner, why-choose-us)
├── contact.html    # Contact form page (Formspree-backed AJAX form)
├── styles.css      # Single shared stylesheet for both pages
├── logo.png        # Brand logo (circular "SRI-ABHISHEK" emblem)
└── CLAUDE.md       # This file
```

## Tech Stack

- **HTML5** — semantic elements (`<nav>`, `<header>`, `<section>`, `<footer>`)
- **CSS3** — flexbox, grid, `clamp()`, `backdrop-filter`, media queries
- **Vanilla JavaScript** — IIFE in `contact.html` for AJAX form submission
- **Formspree** — external service handling form submissions (`https://formspree.io/f/mwvnewbl`)
- **No build step** — files are served as-is; no bundler, preprocessor, or package manager

## Development

### Running locally

Open `index.html` directly in a browser, or serve with any static server:

```sh
python3 -m http.server 8000
# or
npx serve .
```

### No build, lint, or test commands

There is no `package.json`, no linter config, and no test suite. Validation is manual (browser testing).

## Code Conventions

### HTML

- **BEM naming**: `.block__element` and `.block--modifier` (e.g., `.site-nav__brand`, `.section--dark`)
- **ASCII-art comment headers** separate each major section:
  ```html
  <!-- ============================================================
       Section Name — short description
       ============================================================ -->
  ```
- **ARIA attributes** used where appropriate (`aria-label="Primary"`, `role="status"`, `aria-hidden="true"`)
- Navigation and footer markup is duplicated across pages (no templating system)

### CSS (`styles.css`)

- **Apple-inspired design**: generous whitespace, system font stack, pill-shaped buttons
- **Color palette**:
  - Primary blue: `#0071e3` (links, buttons, focus rings)
  - Dark text: `#1d1d1f`
  - Gray text: `#6e6e73`
  - Light bg: `#f5f5f7`
  - Hover blue: `#0077ed`
- **Section variants**: `.section--light` (white), `.section--dark` (charcoal), `.section--gray` (light gray)
- **Responsive breakpoint**: single `@media (max-width: 768px)` for mobile
- **Transitions**: `0.2s ease` for hover states; `0.25s ease` for card lift effects
- **Container**: `.container` constrains to `max-width: 1080px` with `0 auto` centering
- **Comment style**: `/* ---------- Section Name ---------- */` dashed separators

### JavaScript

- Only present in `contact.html` as an inline `<script>` block
- Wrapped in an IIFE `(() => { ... })()` to avoid global scope pollution
- Uses `fetch()` API with `FormData` for AJAX submission to Formspree
- Progressive enhancement: falls back to native form POST if JS is disabled
- Shows `.confirmation.is-visible` on success; `alert()` on error

## Key Patterns

| Pattern | Example |
|---------|---------|
| BEM class names | `.card__title`, `.hero__cta`, `.section--dark` |
| Section structure | `<section class="section section--variant"><div class="container">...</div></section>` |
| Card grid | `.card-grid` with `auto-fit, minmax(280px, 1fr)` |
| Links between pages | Relative paths (`index.html`, `contact.html`) |
| Icons | Unicode entities (`&#10003;`, `&#9776;`) with `aria-hidden="true"` |

## Important Notes

- **No dependencies to install** — no `npm install` or equivalent needed
- **Formspree endpoint** is hardcoded in `contact.html` — changing it requires editing the `action` attribute and the `fetch()` call target
- **Navigation/footer are duplicated** across `index.html` and `contact.html` — changes to shared elements must be applied to both files
- **No CSS custom properties (variables)** — colors are hardcoded hex values throughout `styles.css`
- **Logo** (`logo.png`) is a 533 KB raster image; no SVG version exists
- Copyright year in footer is set to 2026 in both HTML files
