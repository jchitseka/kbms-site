# Eupay - Smart SaaS Billing Tool

Static, self-contained version of the Framer-generated Eupay landing page.

## Structure

```
eupay/
├── index.html                  # Single-page site (homepage)
├── assets/
│   ├── css/
│   │   ├── fonts.css           # @font-face rules (Google Fonts, as in original)
│   │   └── framer.css          # Extracted Framer SSR stylesheet
│   ├── images/                 # All image/favicon assets, descriptive names
│   │   ├── logo.png
│   │   ├── hero-illustration.png
│   │   ├── hero-financial-dashboard.svg
│   │   └── ... (22 assets)
│   └── js/
│       ├── framer/             # Framer runtime modules (53 ESM files,
│       │                       #  including dynamically-imported bundles)
│       ├── vendor/
│       │   └── animator.js     # Framer animation runtime (was inline)
│       └── main.js             # Merged inline scripts (variant + appear + env)
└── favicon/                    # Site favicon set (light/dark/apple-touch)
```

## Origin

The original was a Framer-published single-page site exported as one HTML file
with a flat folder of assets. This project restructures it into a conventional
layout without changing the design, layout, content, or behavior.

### What was changed

- Moved all inline `<style>` blocks into `assets/css/fonts.css` and
  `assets/css/framer.css`.
- Extracted the Framer animator and page bootstrap scripts from inline
  `<script>` tags into `assets/js/vendor/animator.js` and `assets/js/main.js`.
- Downloaded the Framer runtime modules (`assets/js/framer/`) and rewrote all
  `modulepreload`/bundle `src` references to local paths.
- Renamed the image hashes to descriptive kebab-case names and updated all
  `src` references.
- Moved favicons into `favicon/` and switched `<link>` icons to local files.
- Removed editor-only artifacts: the Framer editorbar overlay+styles, the
  `framer_variant` deployment probe, analytics tracker tag, "saved from url"
  comment, and Chromium-extension bridge markup.
- Kept the two `<style data-framer-html-style="">` elements, the
  `data-framer-css-ssr-minified` marker, the `<type="framer/appear">` blocks,
  and `<style type="text/css" data-framer-css="true">` because the Framer
  runtime queries them at boot.
- Fixed the em-dash/newline encoding (the page declared UTF-8; the original
  export stored text with literal UTF-8 multibyte characters).

### What was kept

- All page text, links, images, buttons, forms, animations, responsive
  breakpoints, and interactions are byte-for-byte the original where not
  listed above.
- Brand links to `https://eupay.framer.website/` subpages remain unchanged
  (the only homepage exists locally).
- Google Fonts are still fetched from `fonts.gstatic.com` (unchanged from the
  original).

## Run

No build step or server is required — it is a static site.

- Simply open `index.html` directly in a browser, or
- serve the folder locally, e.g.:

  ```
  npx serve .
  ```
  or with Python:
  ```
  python -m http.server 8080
  ```
  then open `http://localhost:8080`.

Serving locally (rather than opening via `file://`) is recommended so the ES
modules load under a proper origin.