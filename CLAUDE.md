# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

Single-file static landing page for [thegapco.com](https://thegapco.com), deployed via GitHub Pages (`meeglosh/gapco` repo, `main` branch, root). No build step, no dependencies, no package manager.

- **`index.html`** — the entire site: HTML structure, embedded `<style>`, and inline `<script>`
- **`CNAME`** — contains `thegapco.com` for GitHub Pages custom domain routing
- Domain registered on GoDaddy, email (hello@thegapco.com) runs through HostGator (MX records must not be modified)

## Deployment

Edit `index.html`, commit, and push to `main`. GitHub Pages auto-deploys within ~60 seconds. No build or preview server needed — open `index.html` directly in a browser to test locally.

```bash
git add index.html
git commit -m "..."
git push origin main
```

## Design system

All styles are in the `<style>` block at the top of `index.html`. CSS custom properties are defined on `:root`:

| Variable | Value | Usage |
|---|---|---|
| `--navy` | `#0D1B2A` | Primary dark background |
| `--navy-mid` | `#152233` | Ventures section background |
| `--gold` | `#F4C430` | Primary accent, CTAs, pineapple color |
| `--gold-dark` | `#C9A227` | Pineapple texture shadows |
| `--green` | `#2D6A4F` | Contact section background |
| `--green-light` | `#52B788` | Leaf color, live badge, active links |
| `--cream` | `#FDFAF3` | Light section background |
| `--cream-dark` | `#F2ECD8` | Pillar card backgrounds |

**Typography:** Playfair Display (serif, headings/display) + Inter (sans-serif, body). Both loaded from Google Fonts.

**Pineapple SVGs** are inline throughout — nav logo (28×34), hero (110×140 viewBox), footer (20×26). They share the same diamond-grid texture pattern using `--gold-dark` paths with decreasing opacity per row.

## Scroll animations

`.reveal` class marks elements for entrance animation. The `IntersectionObserver` in the `<script>` block adds `.visible` (which transitions opacity and translateY) when elements enter the viewport. Siblings stagger by 90ms based on their index within the parent.

## Venture cards

Each `.vcard` uses a `--accent` CSS custom property (set per-card via inline style or modifier class) that drives the `::before` gradient overlay on hover. Badge variants: `.badge-live` (green) and `.badge-soon` (gold).

## Adding a new venture

1. Add a `.vcard` inside `.ventures-grid` before the `.vcard-more` card
2. Set `--accent` color, icon emoji class (`ico-green`, `ico-gold`, `ico-purple`), badge variant
3. If live, add `is-live` to the `.vcard-link` and link to the real URL
4. Update the "3+" stat in the about section if appropriate
