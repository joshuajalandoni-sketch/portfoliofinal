# ASSETS.md

Every asset in this project: where it lives, its dimensions, and where the site uses it.
Line numbers refer to `index.html`. After moving or renaming any asset, update every
reference to it and update this file.

---

## TODO

- [ ] **Public resume.** Add a redacted resume at `public/files/joshua-jalandoni-resume.pdf`.
      The "Resume ↗" button (line 1345) already points there and returns "not found" until the
      file exists.
- [ ] **favicon.ico fallback.** The site uses an inline SVG monogram (line 26), which modern
      browsers show. Older browsers still want a `favicon.ico`. When it exists, add it at
      `public/favicon.ico` and add a `<link rel="icon">` for it alongside the SVG. Don't add the
      tag before the file exists: a missing icon puts an error in the console.
- [ ] **Hero headshot.** DESIGN.md §6 calls for the processed headshot with the white
      background removed. File TBD.
- [ ] **Client logos.** None exist for Rusty Mule Pizza, Rubens Removal LLC, Pinoy Eats, or Mann
      Cayona, so the "Selected clients" strip shows all four as text wordmarks. To add one, save
      it as `public/images/clients/{client-slug}.{ext}` and set its `logo` in the `CLIENTS` list
      (line 1571). Prefer SVG or a PNG with a transparent background: a logo on a solid white
      square will show as a white tile in dark mode.
- [ ] **Claude Platform 101 certificate is cropped.** The source screenshot starts about 155px
      too low: the top of the certificate (margin and "Certificate of completion" badge) is
      missing, so the file is 950×563 instead of ~950×718. Every copy on disk is identical. The
      official full certificate is a download on its Anthropic Academy (Skilljar) verification
      page, as `verify.skilljar.com/c/…` offers for Cowork. Needs that page's link.
- [ ] **Desktop screenshots.** Full-resolution desktop screenshots are needed for all 5
      projects. The current ones are 1200×750 WebP thumbnails with no originals.
- [ ] **Phone screenshots.** Retake the Rubens Removal and Mann Cayona phone screenshots at the
      top of the page. The current ones are scrolled partway down.
- [ ] **Vercel Output Directory.** Before this branch deploys, confirm the Vercel project's
      Output Directory is set to the project root, not `public/`.

---

## Used on the site

| Path | What it is | Dimensions | Where used |
|---|---|---|---|
| `public/images/hero/headshot.webp` | Headshot | 640×800 | Line 1359: hero photo, front of the work stack |
| `public/images/projects/rusty-mule-pizza-desktop.webp` | Rusty Mule Pizza homepage | 1200×750 | Line 1353: hero work stack (back screenshot). Line 1395: Selected work card. Line 2083: commented-out component demo |
| `public/images/projects/rubens-removal-desktop.webp` | Rubens Removal LLC homepage | 1200×750 | Line 1356: hero work stack (front screenshot). Line 1404: Selected work card |
| `public/images/projects/pinoy-eats-desktop.webp` | Pinoy Eats homepage | 1200×750 | Line 1413: Selected work card |
| `public/images/projects/mann-cayona-desktop.webp` | Mann Cayona homepage | 1200×750 | Line 1422: Selected work card |
| `public/images/projects/berserk-desktop.webp` | Berserk Tribute homepage | 1200×750 | Line 1431: Selected work card |
| `public/images/og-image.jpg` | Link preview card: name, title, headshot | 1200×630 | Lines 32 and 39: `og:image` and `twitter:image`, as `https://jjoshua.vercel.app/public/images/og-image.jpg` |
| `public/files/joshua-jalandoni-resume.pdf` | Public resume | — | Line 1345: "Resume ↗" button. **Missing, see TODO** |

### Certificates

All twelve are listed in the `CERTIFICATES` data (lines 1609–1644) and drawn into the
Certifications section by the script. Each card shows the WebP thumbnail from `thumbs/`
(lazy-loaded); the full image is loaded only when the certificate is opened in the lightbox.
The last seven Anthropic cards start hidden behind "Show all certificates", so their thumbnails
don't load until that button is pressed. (Verified from the browser's network log: a full
page scroll requests 5 thumbnails and no originals; the button adds 7 thumbnails; opening a
certificate requests only that one original.) Titles are exactly as printed. Only the Google
certificate has a printed date; the official Anthropic certificate files have none either.

| Full image (lightbox) | Title as printed | Issuer | Dimensions | Thumbnail (card) |
|---|---|---|---|---|
| `public/images/certifications/google-ai-professional-certificate.jpg` | Google AI Professional Certificate (dated Jun 3, 2026) | Google, via Coursera | 1200×928 | `thumbs/google-ai-professional-certificate.webp`, 600×464 |
| `public/images/certifications/anthropic-claude-101.png` | Claude 101 | Anthropic | 935×714 | `thumbs/anthropic-claude-101.webp`, 600×458 |
| `public/images/certifications/anthropic-claude-code-101.png` | Claude Code 101 | Anthropic | 949×719 | `thumbs/anthropic-claude-code-101.webp`, 600×455 |
| `public/images/certifications/anthropic-claude-platform-101.png` | Claude Platform 101 (top cropped, see TODO) | Anthropic | 950×563 | `thumbs/anthropic-claude-platform-101.webp`, 600×356 |
| `public/images/certifications/anthropic-claude-with-the-anthropic-api.png` | Claude with the Anthropic API | Anthropic | 946×717 | `thumbs/anthropic-claude-with-the-anthropic-api.webp`, 600×455 |
| `public/images/certifications/anthropic-claude-cowork-intro.png` | Introduction to Claude Cowork | Anthropic | 949×718 | `thumbs/anthropic-claude-cowork-intro.webp`, 600×454 |
| `public/images/certifications/anthropic-ai-fluency-ai-capabilities-and-limitations.png` | AI Fluency: AI Capabilities & Limitations | Anthropic | 948×718 | `thumbs/anthropic-ai-fluency-ai-capabilities-and-limitations.webp`, 600×454 |
| `public/images/certifications/anthropic-ai-fluency-for-builders.png` | AI Fluency for Builders (co-branded CodePath) | Anthropic | 949×718 | `thumbs/anthropic-ai-fluency-for-builders.webp`, 600×454 |
| `public/images/certifications/anthropic-ai-fluency-for-small-businesses.png` | AI Fluency for Small Businesses (co-branded PayPal) | Anthropic | 949×718 | `thumbs/anthropic-ai-fluency-for-small-businesses.webp`, 600×454 |
| `public/images/certifications/anthropic-ai-fluency-for-educators.png` | AI Fluency for educators (partner logos: UCC, Ringling College, HEA, National Forum) | Anthropic | 948×720 | `thumbs/anthropic-ai-fluency-for-educators.webp`, 600×456 |
| `public/images/certifications/anthropic-ai-fluency-for-students.png` | AI Fluency for students (same partner logos) | Anthropic | 950×718 | `thumbs/anthropic-ai-fluency-for-students.webp`, 600×453 |
| `public/images/certifications/anthropic-ai-fluency-for-nonprofits.png` | AI Fluency for nonprofits (co-branded GivingTuesday) | Anthropic | 950×719 | `thumbs/anthropic-ai-fluency-for-nonprofits.webp`, 600×454 |

Thumbnails live in `public/images/certifications/thumbs/`: 600px wide WebP, quality 0.82, about
113 KB for all twelve together. They were made from the full images above, so a new certificate
needs a thumbnail of the same name. The Google JPG was rendered from page 1 of
`google-ai-professional-certificate.pdf` at 1200px wide.

Not files:

- **Favicon:** an inline SVG "JJ" monogram on line 26. There is no `favicon.ico` yet (see TODO).
- **Font:** Archivo from Google Fonts, line 45 (preconnects on lines 43–44). One variable
  family; the page requests five width/weight pairs: standard width at 400, 500, 600 and 700,
  and Expanded (125%) at 700 for the hero headline only. Google serves all five from a single
  file, about 88 KB for the Latin subset.
- **Tool icons:** an inline SVG sprite at line 1280, used by the Stack chips: Figma, HTML5, CSS,
  JavaScript, Claude, GitHub, Vercel. Path data from Simple Icons 16.31.0 (CC0), fetched once;
  the page makes no icon requests. The marks remain trademarks of their owners.
- **Client wordmarks:** the four names in the "Selected clients" strip are text, from the
  `CLIENTS` list (line 1571), not image files.

---

## In `public/` but not used on the site yet

| Path | What it is | Dimensions |
|---|---|---|
| `public/images/projects/rusty-mule-pizza-mobile.jpg` | Rusty Mule Pizza on a phone, top of page | 922×2048 |
| `public/images/projects/rubens-removal-mobile.jpg` | Rubens Removal on a phone, scrolled to a service card (see TODO) | 922×2048 |
| `public/images/projects/pinoy-eats-mobile.jpg` | Pinoy Eats on a phone, top of page | 922×2048 |
| `public/images/projects/mann-cayona-mobile.jpg` | Mann Cayona on a phone, scrolled to "The Weave" (see TODO) | 922×2048 |
| `public/images/projects/berserk-mobile.jpg` | Berserk Tribute on a phone, top of page | 922×2048 |
| `public/images/certifications/google-ai-professional-certificate.pdf` | Google AI Professional Certificate (Coursera, 7 courses), the original. The site shows the JPG made from it | PDF, 1 page |
| `public/images/clients/lion-sales-funnels.jpg` | Lion Sales Funnels logo. Held for the Experience section: LSF is an employer, not a web design client, so it is not in the client strip | 200×200 |

---

## Not deployed

These folders are excluded by `.vercelignore`.

### `_source/`: original working files

| Path | What it is | Dimensions |
|---|---|---|
| `_source/certificates/Claude 101.png` | Original of `anthropic-claude-101.png` | 935×714 |
| `_source/certificates/Claude Code 101.png` | Original of `anthropic-claude-code-101.png` | 949×719 |
| `_source/certificates/Claude Platform 101.png` | Original of `anthropic-claude-platform-101.png` | 950×563 |
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

80 PNGs of the site taken during the redesign, in `before/`, `phase1/`, `phase2/`,
`foundation-before/`, `foundation-after/`, and `sections-after/`, at phone, tablet, and desktop
widths. The `foundation-*` and `sections-after` folders cover 360, 768, 1024, and 1440 in both
themes, fold and full page, and each holds a `metrics.json` with page height, heading sizes, and
section gaps. `foundation-after/` doubles as the "before" set for `sections-after/`. Also
excluded from git by `.gitignore`.

---

## Outside this project

Files with personal data (IP address, earnings, account data, the full resume, personal
photos) are kept in `../jjoshua-private/`, outside this repository. They are not part of the
site.
