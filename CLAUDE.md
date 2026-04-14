# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal portfolio website for Carlos Muñoz (cmunozgar.com). Pure HTML5, CSS3, and vanilla ES6+ JavaScript — no build step, no framework, no transpilation. Deployed via GitHub Pages.

## Development

```bash
npm install   # First time only
npm start     # Start dev server with live reload at http://localhost:3000
```

Gulp + BrowserSync watches `*.html`, `**/*.html`, `styles.css`, `script.js`, and `partials/*.html` for changes.

## Architecture

### Component Loading

Pages don't repeat shared markup. Instead, `assets/js/script.js` fetches three HTML partials at runtime and injects them into every page:

- `partials/banner.html` — Twitter/X-style profile card
- `partials/nav.html` — navigation menu
- `partials/footer.html` — footer

The script resolves relative paths based on directory depth (root vs. subdirectory pages) and injects page-specific content into the banner after loading.

### Theming

- CSS custom properties defined in `assets/css/styles.css` under `:root` (light) and `[data-theme="dark"]` selectors
- `assets/js/theme-init.js` runs synchronously in `<head>` to apply the stored theme before paint (prevents flash)
- `script.js` handles the toggle button and persists the choice to `localStorage`

### Page Structure

Pages live at root (`index.html`) or in subdirectories (`about/`, `articles/`, `updates/`). Each page follows the same shell pattern — it loads the shared partials and defines its own content section.

### Key Files

| File | Purpose |
|------|---------|
| `assets/js/script.js` | All runtime logic: partial loading, theme toggle, like/share buttons, banner content |
| `assets/js/theme-init.js` | Synchronous theme bootstrap (in `<head>`) |
| `assets/css/styles.css` | All styles including CSS variable definitions for both themes |
| `gulpfile.js` | Dev server config (BrowserSync on port 3000, watches for live reload) |
