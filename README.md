# Bearo Casino — HUGO landing

Pure HUGO static site for **bearo.si** (sl-SI, EUR). Tailwind via CDN, custom CSS for jelly/candy aesthetic, Font Awesome for icons. No React, no Next, no build step beyond `hugo`.

## Project layout

```
bearo/si/
├── hugo.toml                  # site config, menus, params
├── content/
│   ├── _index.md              # homepage front matter (template lives in layouts/index.html)
│   ├── odgovorno-igranje.md
│   ├── pravila-bonusov.md
│   ├── pogoji.md
│   └── zasebnost.md
├── layouts/
│   ├── _default/
│   │   ├── baseof.html        # base shell
│   │   ├── single.html        # rendered for every .md page
│   │   └── list.html
│   ├── partials/
│   │   ├── head.html          # all SEO + structured data + Tailwind config
│   │   ├── nav.html           # sticky candy nav with mobile fold
│   │   └── footer.html        # deep plum footer with responsible-gambling block
│   └── index.html             # homepage sections (hero, bonusi, igre, vip, plačila, trust, FAQ, CTA)
└── static/
    ├── css/custom.css         # 100% of jelly visuals, animations, tabs, hover lifts
    └── robots.txt
```

## Run locally

```bash
# install Hugo (extended is fine, but not required here)
brew install hugo            # macOS
# or grab a binary from https://github.com/gohugoio/hugo/releases

cd bearo/si
hugo server -D --disableFastRender
# open http://localhost:1313/
```

## Build for production

```bash
cd bearo/si
hugo --minify
# output goes to ./public — upload that to your host (Netlify, Vercel, Cloudflare Pages, plain S3 + CloudFront, etc.)
```

Set `baseURL` in `hugo.toml` to the real domain before build (currently `https://bearo.si/`).

## What's already wired

- **SEO** — meta title/description, canonical, Open Graph, Twitter cards. JSON-LD for `WebSite`, `Organization`, `FAQPage`. Slovenian locale (`sl_SI`).
- **Sticky nav** with semi-transparent cream background, candy logo mark and a CSS-only mobile menu (`<details>`).
- **Hero** with floating jelly bear SVG, animated blobs, neon dotted rings, and a pinned bonus banner.
- **Bonus section** — main bonus card (200% / €7.000 / 25 FS / 5% cashback) and secondary card (100% / €750 / 200 FS).
- **Games** — CSS-only tabs (radio inputs + sibling selectors) with five categories: Igralni avtomati, Ruleta, Blackjack, Live Casino, Jackpoti.
- **VIP** — four tiers: Candy Bronze, Jelly Silver, Sugar Gold, Neon Diamond.
- **Plačila** — Visa, Mastercard, bančno nakazilo, Skrill, Neteller, Paysafecard, Apple Pay, Google Pay.
- **Trust** — 6 badges including odgovorno igranje and varstvo podatkov.
- **FAQ** — `<details>` accordion, JSON-LD-mirrored.
- **Footer** — deep plum gradient, social, legal, responsible-gambling 18+ block.

## Tweaking

- **Bonus copy / numbers** live in `hugo.toml` under `[params]` and inline in `layouts/index.html` (for the visible card titles).
- **Game tiles** are defined inline as Hugo `slice` literals in `layouts/index.html` — replace with real game names + icons whenever you want, no template change needed.
- **Color palette** — `:root` block at the top of `static/css/custom.css`. Tailwind reads the same palette via the `tailwind.config` block in `layouts/partials/head.html`, so `bg-raspberry`, `text-mint`, etc. are available everywhere if you want to layer utilities.
- **Logo** — inline SVG in `nav.html` and `footer.html`. To swap, replace both `<svg>` blocks (or extract them into a single partial).

## Notes on “no JS”

Tailwind is loaded via the official Play CDN (`cdn.tailwindcss.com`), which is itself a small JS shim. If strict zero-JS is required, swap that line for a precompiled Tailwind CSS file (or remove it; the layout still works because all visuals live in `custom.css`). Smooth scrolling, tabs, mobile menu, FAQ — all CSS-only.

## Responsible gambling / compliance

The site is built for the Slovenian market (sl-SI, EUR). Every section that mentions bonuses repeats the wagering disclaimer; the footer carries a permanent 18+ block and links to `/odgovorno-igranje/`. Update those texts to match the exact wording your operator uses before launch.
