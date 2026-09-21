# Pixel Forge — Game Showcase

A single-page, self-contained website for showcasing indie games — trailers, screenshots, descriptions, and links to where people can play them. No backend, no database, no login. Everything lives in one `index.html` file, which makes it free to host and trivial to deploy.

**Live site:** https://adhiraj-shukla.github.io/PixelForge.github.io/

## How it works

The entire site — styling, layout, and content — is contained in `index.html`. There is nothing to install and nothing to build. Open the file in a browser and it runs; push it to GitHub Pages (or any static host) and it's live.

All of the editable content lives in two plain JavaScript objects near the top of the `<script>` tag:

- **`SITE`** — your studio name, tagline, hero text, bio, contact email, and social/store links.
- **`GAMES`** — a list of your games. Each one controls a card on the shelf, an entry in the detail popup, and (if `featured: true`) the hero banner.

There is intentionally no admin panel or login. Editing the site means editing this file directly — either locally or straight in GitHub's web editor — and committing the change.

## Adding a game

1. Open `index.html` on GitHub and click the pencil icon to edit it in your browser.
2. Find `const GAMES = [` and add a new entry, following this shape:

   ```js
   {
     id: 'unique-id-for-this-game',       // any short unique string, no spaces
     title: 'Game Title',
     tagline: 'A short, punchy one-liner shown on the card.',
     description: 'A longer description shown when someone opens the game.',
     status: 'released',                   // 'released' | 'development' | 'prototype'
     genre: 'Platformer',                  // powers the filter chips above the shelf
     coverUrl: 'https://.../cover.png',    // hosted image link (imgur, itch.io, etc.)
     videoUrl: 'https://youtu.be/xxxxxxxx',// YouTube, Vimeo, or a direct .mp4 link — optional
     screenshots: [
       'https://.../shot1.png',
       'https://.../shot2.png',
     ],
     platforms: [
       { label: 'Play on itch.io', url: 'https://yourname.itch.io/game' },
     ],
     published: true,                      // false = hidden from the site (a draft)
     featured: false,                      // true = shown in the hero (only set this on one game)
   },
   ```

3. Commit the change directly to the `main` branch. GitHub Pages usually rebuilds within a minute.

**Note:** all image/video links must point to files already hosted somewhere (imgur, itch.io, YouTube, your own site, etc.) — this project doesn't host media itself.

## Editing site info

At the top of `const SITE = { ... }`, update:

- `storeName`, `tagline` — shown in the header and browser tab title.
- `heroHeadline`, `heroSub` — the text above the featured game's trailer.
- `portraitUrl`, `aboutText` — your photo/logo and bio in the About section.
- `contactEmail`, `contactSub` — the Get in Touch section.
- `socialLinks` — an array of `{ label, url }` pairs (itch.io, Twitter/X, Discord, etc.).

## Local preview

No build step needed — just open `index.html` directly in a browser, or serve it locally:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deploying

This repo is already set up for GitHub Pages, serving `index.html` from the root of the `main` branch. To update the live site, edit `index.html` and push/commit to `main` — no separate build or deploy step is required.

## Tech notes

- Single HTML file: HTML, CSS, and JavaScript all inline, no external JS frameworks or build tools.
- Fonts loaded from Google Fonts (`Press Start 2P`, `Space Grotesk`).
- Fully static — no server, no storage, no tracking.
