# ASSETS.md

Every asset in this project: where it lives, its dimensions, and where the site uses it.
Line numbers refer to `index.html`. After moving or renaming any asset, update every
reference to it and update this file.

---

## TODO

- [ ] **favicon.ico fallback.** The site uses an inline SVG monogram (line 27), which modern
      browsers show. Older browsers still want a `favicon.ico`. When it exists, add it at
      `public/favicon.ico` and add a `<link rel="icon">` for it alongside the SVG. Don't add the
      tag before the file exists: a missing icon puts an error in the console.
- [ ] **Light versions of two Experience logos.** On the dark page, the navy Capital One wordmark
      measures a median 1.2:1 at rest (1.52:1 in full color) and VA House's black stroke 1.44:1,
      so both nearly vanish. Save reversed (light) versions and point `EXPERIENCE` at them, or
      swap per theme. Permission to show all five logos is an open decision (DESIGN.md §12).
- [ ] **Link preview image still shows the old headshot.** `og-image.jpg` was composed with the
      white-background headshot, which the hero no longer uses. Rebuild it with
      `joshua-at-desk.webp` if the preview should match the page.
- [ ] **Brand logos, to be supplied by Joshua.** The "Brands I've worked with" band (after
      Experience) has no logos yet, so it's hidden. For each company he worked for or with and has
      permission to show, save the logo as `public/images/brands/{brand-slug}.svg` (or `.png`)
      and add one object to the `BRANDS` list (line 1774): name, src, the file's real width and
      height, and an optional scale. It must be a one-color SVG or a PNG with a transparent
      background: the page paints it in `--muted` through a mask, so a JPG, or a logo on a solid
      background, would show as a solid rectangle. That rules out `lion-sales-funnels.jpg` as it
      is. Roblox and American Express logos are never used (no permission; see DESIGN.md §6).
- [ ] **Desktop screenshots.** Full-resolution desktop screenshots are needed for all 5
      projects. The current ones are 1200×750 WebP thumbnails with no originals. They're now
      preloaded on desktop for the Selected work preview: 204 KB for all five, and
      `rubens-removal-desktop.webp` is 101 KB of it, about half. When the Rubens Removal
      screenshot is retaken, re-export it smaller.
- [ ] **Phone screenshots.** Retake the Rubens Removal and Mann Cayona phone screenshots at the
      top of the page. The current ones are scrolled partway down, and they now show on the
      Selected work cards from 768px. Save the retake in `_source/images/` and regenerate the
      360px WebP in `public/images/projects/`.
- [ ] **Vercel Output Directory.** Before this branch deploys, confirm the Vercel project's
      Output Directory is set to the project root, not `public/`.

---

## Used on the site

| Path | What it is | Dimensions | Where used |
|---|---|---|---|
| `public/images/jj-illustration.webp` | Line illustration of Joshua in a red, yellow, and green cap, transparent. 2x export of `_source/images/jj-illustration.png`, uncropped, WebP quality 0.9 | 295×400, 35 KB | About, top of the side column: 200px tall on a light tile |
| `public/logos/lion-sales-funnels.png` | Lion Sales Funnels mark: blue crowned lion head, transparent | 306×426, 184 KB | Experience, Claude Operator entry: 16×22 (a mark) |
| `public/logos/roblox.png` | Roblox app icon: blue rounded square, white tilted square | 512×512, 28 KB | Experience, Game Advisor entry: 22×22 (a mark) |
| `public/logos/va-house.png` | VA House PH mark: orange, black, and blue strokes, transparent | 357×174, 18 KB | Experience, Virtual Assistant entry: 44×21 (a mark). Black stroke barely shows in dark (see TODO) |
| `public/logos/amex.svg` | American Express blue box logo (2018) | 1000×998, 17 KB | Experience, Customer Data & Support entry: 22×22 (a mark). Its lettering is about 3.5px tall there, unreadable |
| `public/logos/capital-one.png` | Capital One wordmark, navy with red swoosh, transparent | 960×345, 45 KB | Experience, Customer Service Specialist entry: 78×28 (a wordmark). Barely shows in dark (see TODO) |
| `public/images/hero/joshua-at-desk.webp` | Joshua at his desk, monitor, PC, and laptop behind him. 4:5 crop (x 80, y 493, 1244×1555) of `_source/images/joshua-at-desk.png`, WebP quality 0.72, no metadata | 736×920, 52 KB | Hero portrait (the hero's `<img>`), 2x its 368×460 box |
| `public/images/projects/rusty-mule-pizza-desktop.webp` | Rusty Mule Pizza homepage | 1200×750, 38 KB | Line 2051: `PROJECTS` data, Selected work card screenshot and the desktop list's hover preview. Line 3080: commented-out component demo |
| `public/images/projects/rusty-mule-pizza-mobile.webp` | Rusty Mule Pizza on a phone, top of page | 360×800 | Line 2052: `PROJECTS` data, phone screenshot on the card from 768px |
| `public/images/projects/rubens-removal-desktop.webp` | Rubens Removal LLC homepage | 1200×750, 101 KB (see TODO) | Line 2057: `PROJECTS` data, Selected work card screenshot and the desktop list's hover preview |
| `public/images/projects/rubens-removal-mobile.webp` | Rubens Removal on a phone, scrolled to a service card (see TODO) | 360×800 | Line 2058: `PROJECTS` data, phone screenshot on the card from 768px |
| `public/images/projects/pinoy-eats-desktop.webp` | Pinoy Eats homepage | 1200×750, 37 KB | Line 2063: `PROJECTS` data, Selected work card screenshot and the desktop list's hover preview |
| `public/images/projects/pinoy-eats-mobile.webp` | Pinoy Eats on a phone, top of page | 360×800 | Line 2064: `PROJECTS` data, phone screenshot on the card from 768px |
| `public/images/projects/mann-cayona-desktop.webp` | Mann Cayona homepage | 1200×750, 20 KB | Line 2069: `PROJECTS` data, Selected work card screenshot and the desktop list's hover preview |
| `public/images/projects/mann-cayona-mobile.webp` | Mann Cayona on a phone, scrolled to "The Weave" (see TODO) | 360×800 | Line 2070: `PROJECTS` data, phone screenshot on the card from 768px |
| `public/images/projects/berserk-desktop.webp` | Berserk Tribute homepage | 1200×750, 14 KB | Not referenced. Berserk is on the Personal projects line below Selected work, which has no screenshot or hover preview, so its screenshots were taken out of `PROJECTS`. Kept in case it ever returns as a card |
| `public/images/projects/berserk-mobile.webp` | Berserk Tribute on a phone, top of page | 360×800 | Not referenced, as above |
| `public/images/og-image.jpg` | Link preview card: name, title, headshot, in the sage and bone light tokens (`--ink` ground, `--text` name, `--muted` title, `--accent` rule, `--accent-text` address). Same layout and headshot as the indigo version it replaced | 1200×630, 53 KB | Lines 33 and 40: `og:image` and `twitter:image`, as `https://jjoshua.vercel.app/public/images/og-image.jpg` |
| `public/files/joshua-jalandoni-resume.pdf` | Public resume, redacted: contact details read "available on request". No email, phone number, address, or links anywhere in it; the PDF's metadata holds only the name and the title "Joshua Jalandoni - Resume". Names Lion Sales Funnels, so the `[VERIFY]` in CONTENT.md covers it. Moved from the project root | 5,363 bytes (5.2 KB), 2 pages, A4 | Line 1508: "Resume ↗" button (checked: returns the PDF) |

The phone screenshots are 360px WebP copies made from the 922×2048 originals, which are now in
`_source/images/`. Project images on the cards load lazily. On a screen at least 1024px wide with
a mouse or trackpad, the cards aren't shown, so their images never load; instead the five desktop
screenshots load once the page has finished loading, for the list's hover preview. Phones and
touch screens never load the preview copies.

### Certificates

All twelve are listed in the `CERTIFICATES` data (lines 1823–1870) and drawn into the
Certifications section by the script. Each card shows the WebP thumbnail from `thumbs/`
(lazy-loaded); the full image is loaded only when the certificate is opened in the lightbox.
The last seven Anthropic cards start hidden behind "Show all certificates", so their thumbnails
don't load until that button is pressed. (Verified from the browser's network log: a full
page scroll requests 5 thumbnails and no originals; the button adds 7 thumbnails; opening a
certificate requests only that one original.) Titles are exactly as printed. Only the Google
certificate has a printed date; the official Anthropic certificate files have none either.
Each entry's `verifyUrl` is a link, not a file: all twelve point to the issuer's verification
page, listed in CONTENT.md.

| Full image (lightbox) | Title as printed | Issuer | Dimensions | Thumbnail (card) |
|---|---|---|---|---|
| `public/images/certifications/google-ai-professional-certificate.jpg` | Google AI Professional Certificate (dated Jun 3, 2026) | Google, via Coursera | 1200×928 | `thumbs/google-ai-professional-certificate.webp`, 600×464 |
| `public/images/certifications/anthropic-claude-101.png` | Claude 101 | Anthropic | 935×714 | `thumbs/anthropic-claude-101.webp`, 600×458 |
| `public/images/certifications/anthropic-claude-code-101.png` | Claude Code 101 | Anthropic | 949×719 | `thumbs/anthropic-claude-code-101.webp`, 600×455 |
| `public/images/certifications/anthropic-claude-platform-101.jpg` | Claude Platform 101 (from the official certificate, see below) | Anthropic | 1200×909 | `thumbs/anthropic-claude-platform-101.webp`, 600×455 |
| `public/images/certifications/anthropic-claude-with-the-anthropic-api.png` | Claude with the Anthropic API | Anthropic | 946×717 | `thumbs/anthropic-claude-with-the-anthropic-api.webp`, 600×455 |
| `public/images/certifications/anthropic-claude-cowork-intro.png` | Introduction to Claude Cowork | Anthropic | 949×718 | `thumbs/anthropic-claude-cowork-intro.webp`, 600×454 |
| `public/images/certifications/anthropic-ai-fluency-ai-capabilities-and-limitations.png` | AI Fluency: AI Capabilities & Limitations | Anthropic | 948×718 | `thumbs/anthropic-ai-fluency-ai-capabilities-and-limitations.webp`, 600×454 |
| `public/images/certifications/anthropic-ai-fluency-for-builders.png` | AI Fluency for Builders (co-branded CodePath) | Anthropic | 949×718 | `thumbs/anthropic-ai-fluency-for-builders.webp`, 600×454 |
| `public/images/certifications/anthropic-ai-fluency-for-small-businesses.png` | AI Fluency for Small Businesses (co-branded PayPal) | Anthropic | 949×718 | `thumbs/anthropic-ai-fluency-for-small-businesses.webp`, 600×454 |
| `public/images/certifications/anthropic-ai-fluency-for-educators.png` | AI Fluency for educators (partner logos: UCC, Ringling College, HEA, National Forum) | Anthropic | 948×720 | `thumbs/anthropic-ai-fluency-for-educators.webp`, 600×456 |
| `public/images/certifications/anthropic-ai-fluency-for-students.png` | AI Fluency for students (same partner logos) | Anthropic | 950×718 | `thumbs/anthropic-ai-fluency-for-students.webp`, 600×453 |
| `public/images/certifications/anthropic-ai-fluency-for-nonprofits.png` | AI Fluency for nonprofits (co-branded GivingTuesday) | Anthropic | 950×719 | `thumbs/anthropic-ai-fluency-for-nonprofits.webp`, 600×454 |

Thumbnails live in `public/images/certifications/thumbs/`: 600px wide WebP, quality 0.82, about
114 KB for all twelve together. They were made from the full images above, so a new certificate
needs a thumbnail of the same name. The Google JPG was rendered from page 1 of
`google-ai-professional-certificate.pdf` at 1200px wide.

The Claude Platform 101 JPG replaces a screenshot whose top was cut off. It was made from the
official certificate image on its verification page (3300×2550, kept in `_source/certificates/`):
the white print margin around the colored certificate was trimmed, as the other Anthropic
screenshots show no margin, then it was scaled to 1200px wide at JPEG quality 0.9. The
trimmed certificate is 1.320:1, the same shape as the others. The cropped PNG and its thumbnail
are in `_archive/`.

Not files:

- **Favicon:** an inline SVG "JJ" monogram on line 26. There is no `favicon.ico` yet (see TODO).
- **Font:** Archivo from Google Fonts, line 45 (preconnects on lines 43–44). One variable
  family; the page requests five width/weight pairs: standard width at 400, 500, 600 and 700,
  and Expanded (125%) at 700 for the hero headline only. Google serves all five from a single
  file, about 88 KB for the Latin subset.
- **Tool icons:** an inline SVG sprite at the bottom of the page (line 2716), used by the
  Stack tool tiles through the `STACK` list (line 1779) and by the tools marquee through the
  `TOOL_LOGOS` list (line 1750). 22 symbols, each downloaded once, so the page makes no icon
  requests; every mark remains a trademark of its owner.
  - Simple Icons 16.31.0, CC0 unless noted: JavaScript (MIT), HTML5, CSS, React, Tailwind CSS,
    n8n, Claude (used for Claude API), Google Gemini, Google Sheets, Google Drive, Google
    Calendar, Vercel, Cloudflare, Git (CC BY 3.0), Docker, Forgejo (CC BY-SA 4.0), Authentik,
    Figma, Leaflet, GitHub. The licensed three are credited, with their sources, in the
    sprite's comment.
  - Devicon 2.17.0 (MIT): Slack, the one-color "plain" version.
  - `icon-placeholder`: a dashed circle drawn for this site, shown for the two tools with no
    official icon in either library, **OpenAI API** and **Excel**. It isn't an approximation of
    either logo.
  - GitHub is back for the tools marquee, restored byte for byte from the 13 September
    download rather than fetched again.
  - The marquee shows ten of these: Cloudflare, Figma, GitHub, Vercel, Claude, Gemini, n8n,
    Docker, Slack, Leaflet. OpenAI and Google Workspace are on its approved list but have no
    icon in Simple Icons or Devicon, so they aren't shown (no placeholder in a logo row).
- **Selected clients strip: removed.** It repeated the client names already on the Selected work
  cards. Nothing on the page references `public/images/clients/` any more; the folder and
  `lion-sales-funnels.jpg` stay, in case Experience uses the logo later.
- **Brand logos:** none yet. The band reads them from `public/images/brands/` through the
  `BRANDS` list (line 1774) once they're supplied (see TODO).
- **Project tech chips and Experience text** are text from the `PROJECTS` (line 1883) and
  `EXPERIENCE` (line 1926) lists; the hero stats come from `STATS` (line 1955). No Experience
  entry shows a logo: Lion Sales Funnels is text only (see below), and Roblox and American
  Express logos are never used, as there's no permission to use those trademarks.

---

## In `public/` but not used on the site yet

| Path | What it is | Dimensions |
|---|---|---|
| `public/images/certifications/google-ai-professional-certificate.pdf` | Google AI Professional Certificate (Coursera, 7 courses), the original. The site shows the JPG made from it | PDF, 1 page |
| `public/images/clients/lion-sales-funnels.jpg` | Lion Sales Funnels logo, on a solid white square. Tried in the Experience timeline at 72px and taken out: in dark mode it reads as a bright white tile, the brightest thing on that part of the page. The company name shows as text instead. A version with a transparent background could go in the same slot (`logo` in the `EXPERIENCE` list, line 1926). Kept text only again when Experience grew to seven entries. No section references `public/images/clients/` now that the Selected clients strip is gone; the file is kept for a possible Experience logo. As a solid-background JPG it can't be used in the Brands band. Naming Lion Sales Funnels publicly is still `[VERIFY]` in CONTENT.md | 200×200 |

---

## Not deployed

These folders are excluded by `.vercelignore`.

### `_source/`: original working files

| Path | What it is | Dimensions |
|---|---|---|
| `_source/certificates/Claude 101.png` | Original of `anthropic-claude-101.png` | 935×714 |
| `_source/certificates/Claude Code 101.png` | Original of `anthropic-claude-code-101.png` | 949×719 |
| `_source/certificates/Claude Platform 101.png` | Screenshot of Claude Platform 101 with the top cut off; was the site's copy until replaced by the official file below | 950×563 |
| `_source/certificates/certificate-tasao5euiu3h-1782864848.jpg` | Official Claude Platform 101 certificate, saved from its verification page (`verify.skilljar.com/c/tasao5euiu3h`) under the issuer's file name. Original of `anthropic-claude-platform-101.jpg` | 3300×2550 |
| `_source/certificates/Claude Cowork.png` | Original of `anthropic-claude-cowork-intro.png` | 949×718 |
| `_source/certificates/Screenshot 2026-07-08 202657.png` | Original of `anthropic-claude-with-the-anthropic-api.png` | 946×717 |
| `_source/certificates/Screenshot 2026-07-08 210411.png` | Original of `anthropic-ai-fluency-for-nonprofits.png` | 950×719 |
| `_source/certificates/Screenshot 2026-07-08 210530.png` | Original of `anthropic-ai-fluency-for-students.png` | 950×718 |
| `_source/certificates/Screenshot 2026-07-08 210609.png` | Original of `anthropic-ai-fluency-for-educators.png` | 948×720 |
| `_source/certificates/Screenshot 2026-07-09 095036.png` | Original of `anthropic-ai-fluency-for-small-businesses.png` | 949×718 |
| `_source/certificates/Screenshot 2026-07-09 095103.png` | Original of `anthropic-ai-fluency-for-builders.png` | 949×718 |
| `_source/certificates/Screenshot 2026-07-09 095128.png` | Original of `anthropic-ai-fluency-ai-capabilities-and-limitations.png` | 948×718 |
| `_source/certificates/JoshuaJalandoni_AIFundamentals_Cert.pdf` | Original of `google-ai-professional-certificate.pdf` | PDF, 1 page |
| `_source/images/me.jpg` | Headshot, square crop | 400×400 |
| `_source/images/jj-illustration.png` | Original of `jj-illustration.webp`, found as `public/images/jj-illustration.png.png` | 609×826, 432 KB |
| `_source/images/joshua-at-desk.png` | Original of `joshua-at-desk.webp`: desk selfie, found in the project root as `hero-desk.jpg.png` (a PNG despite the name) | 1540×2048, 2.9 MB |
| `_source/images/rusty-mule-pizza-mobile.jpg` | Original of `rusty-mule-pizza-mobile.webp` (moved from `public/`) | 922×2048 |
| `_source/images/rubens-removal-mobile.jpg` | Original of `rubens-removal-mobile.webp` (moved from `public/`) | 922×2048 |
| `_source/images/pinoy-eats-mobile.jpg` | Original of `pinoy-eats-mobile.webp` (moved from `public/`) | 922×2048 |
| `_source/images/mann-cayona-mobile.jpg` | Original of `mann-cayona-mobile.webp` (moved from `public/`) | 922×2048 |
| `_source/images/berserk-mobile.jpg` | Original of `berserk-mobile.webp` (moved from `public/`) | 922×2048 |
| `_source/images/Screenshot 2026-09-11 175158.png` | Rubens Removal, mid-page section | 1887×891 |
| `_source/images/Screenshot 2026-09-11 175309.png` | Rusty Mule Pizza, "Friday Night Specials" section | 1615×890 |
| `_source/images/Screenshot 2026-09-11 175501.png` | Pinoy Eats, food photo carousel | 1852×828 |
| `_source/images/Google-Cloud-Logo.png` | Google Cloud logo | 3840×2160 |
| `_source/images/Logo_of_YouTube_(2015-2017).svg.webp` | YouTube logo, 2015–2017 version | 3840×1603 |

The seven `Screenshot 2026-07-0…` certificates were copied (not moved) from
`Desktop\Desktop\Website Projects\Jalandoni Developments\assets\img\`, where the originals remain.
That folder also holds identical copies of the first four certificates.

### `_archive/`: unused files kept for reference

| Path | What it is | Dimensions |
|---|---|---|
| `_archive/headshot.jpg` | JPEG copy of the headshot | 640×800 |
| `_archive/headshot.webp` | The former hero headshot, white background (moved from `public/images/hero/headshot.webp` when the desk photo replaced it) | 640×800 |
| `_archive/og-image-indigo.jpg` | The former link preview image, in the indigo palette (moved from `public/images/og-image.jpg`) | 1200×630 |
| `_archive/anthropic-claude-platform-101-cropped.png` | The site's former Claude Platform 101 image, top cut off (moved from `public/images/certifications/anthropic-claude-platform-101.png`) | 950×563 |
| `_archive/anthropic-claude-platform-101-cropped-thumb.webp` | Its former card thumbnail (moved from `thumbs/anthropic-claude-platform-101.webp`) | 600×356 |
| `_archive/game-ambassador-client-review.png` | 5-star client review, game ambassador role | 742×237 |
| `_archive/gatherr-app-prototype.png` | Gatherr app prototype preview | 1290×765 |
| `_archive/gatherr-app-code-editor.png` | Gatherr app source code in an editor | 1357×891 |
| `_archive/pulaw-focus-app.png` | Pulaw focus-timer app | 1321×765 |
| `_archive/pulaw-focus-app-code-editor.png` | Source code of a focus/co-working app, likely Pulaw | 1376×769 |
| `_archive/typing-test-97-wpm-summary.png` | Typing test result, summary | 1120×488 |
| `_archive/typing-test-97-wpm-details.png` | Typing test result, details | 1591×758 |
| `_archive/highlevel-logo.png` | HighLevel logo | 4929×1690 |
| `_archive/duplicates/` | Exact copies of six files above, same names | — |
| `_archive/empty-google-drive-download/` | An empty folder from a Google Drive download | — |

### `.screenshots/`: redesign captures

96 PNGs of the site taken during the redesign, in `before/`, `phase1/`, `phase2/`,
`foundation-before/`, `foundation-after/`, `sections-after/`, and `content-after/`, at phone,
tablet, and desktop widths. The `foundation-*`, `sections-after`, and `content-after` folders
cover 360, 768, 1024, and 1440 in both themes, fold and full page, and each holds a
`metrics.json` with page height, heading sizes, and section gaps. Each "after" set doubles as the
"before" set for the next. Also excluded from git by `.gitignore`.

---

## Outside this project

Files with personal data (IP address, earnings, account data, the full resume, personal
photos) are kept in `../jjoshua-private/`, outside this repository. They are not part of the
site.
