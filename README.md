# Joshua Jalandoni — Portfolio

Personal portfolio site. Web design and development work for small businesses, built from
Bacolod City, Philippines.

**Live:** https://jjoshua.vercel.app

---

## Stack

Static HTML, CSS, and JavaScript. No framework, no build step, no bundler — this is
deliberate. Open `index.html` in a browser and it runs.

- Fonts: Archivo (Google Fonts)
- Hosting: Vercel, auto-deploying from this repository

---

## Running locally

Open `index.html` directly, or serve the folder:

```bash
python3 -m http.server 8000
```

Then visit `http://localhost:8000`.

---

## Structure

```
/
├── index.html          Single-page site
├── DESIGN.md           Design system — read before changing anything visual
├── CLAUDE.md           Instructions for Claude Code
├── ASSETS.md           Asset manifest: what each file is and where it's used
├── README.md
├── public/
│   ├── images/
│   │   ├── hero/            Headshot and portrait images
│   │   ├── projects/        Website screenshots, desktop and mobile
│   │   ├── certifications/  Certificate images
│   │   ├── clients/         Client and employer logos
│   │   └── og-image.png     Link preview image, 1200×630
│   ├── files/               Resume and other downloads
│   └── favicon.ico
├── _source/            Working files, not deployed
└── _archive/           Unused files kept for reference, not deployed
```

---

## Conventions

**Filenames** are lowercase with hyphens. No spaces, dates, UUIDs, or `(1)` suffixes.

- Projects: `rusty-mule-pizza-desktop.png`
- Certificates: `anthropic-claude-code-101.jpg`
- Clients: `rubens-removal.png`

**Design values** — colors, type sizes, spacing, radii — come from CSS custom properties.
Nothing is hardcoded. The full token set is in `DESIGN.md`.

**Content data** for projects, certifications, and experience lives in JS arrays rendered by
template functions, so adding an item means adding one object.

---

## Work featured here

| Project | Client type | Live |
|---|---|---|
| Rusty Mule Pizza | Wood-fired pizzeria, Karnack, Texas | rustymulepizza.vercel.app |
| Rubens Removal LLC | Land clearing, Florida | rubensremoval-llc.vercel.app |
| Pinoy Eats | Filipino home kitchen, Greenville, Texas | pinoyeats.vercel.app |
| Mann Cayona | Visual artist, Iloilo City | manncayona.vercel.app |
| Berserk Tribute | Personal project | berserk-jj.vercel.app |

---

## Deployment

Pushing to the default branch triggers a Vercel deploy. Check the preview before merging
anything significant.

---

## Before adding an image

1. Convert to WebP
2. Resize to roughly the dimensions it displays at — don't ship a 4000px file for a 600px slot
3. Name it per the conventions above
4. Put it in the right `public/images/` subfolder
5. Add `alt` text and explicit `width`/`height`
6. Add a row to `ASSETS.md`

---

## Contact

Joshua Jalandoni — Bacolod City, Philippines
