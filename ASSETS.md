# ASSETS.md

Every asset in this project: where it lives, its dimensions, and where the site uses it.
Line numbers refer to `index.html`. After moving or renaming any asset, update every
reference to it and update this file.

---

## TODO

- [ ] **Public resume.** Add a redacted resume at `public/files/joshua-jalandoni-resume.pdf`.
      The "Resume ↗" button (line 1082) already points there and returns "not found" until the
      file exists.
- [ ] **favicon.ico fallback.** The site uses an inline SVG monogram (line 26), which modern
      browsers show. Older browsers still want a `favicon.ico`. When it exists, add it at
      `public/favicon.ico` and add a `<link rel="icon">` for it alongside the SVG. Don't add the
      tag before the file exists: a missing icon puts an error in the console.
- [ ] **Hero headshot.** DESIGN.md §6 calls for the processed headshot with the white
      background removed. File TBD.
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
| `public/images/hero/headshot.webp` | Headshot | 640×800 | Line 1096: hero photo, front of the work stack |
| `public/images/projects/rusty-mule-pizza-desktop.webp` | Rusty Mule Pizza homepage | 1200×750 | Line 1090: hero work stack (back screenshot). Line 1137: Selected work card. Line 1497: commented-out component demo |
| `public/images/projects/rubens-removal-desktop.webp` | Rubens Removal LLC homepage | 1200×750 | Line 1093: hero work stack (front screenshot). Line 1146: Selected work card |
| `public/images/projects/pinoy-eats-desktop.webp` | Pinoy Eats homepage | 1200×750 | Line 1155: Selected work card |
| `public/images/projects/mann-cayona-desktop.webp` | Mann Cayona homepage | 1200×750 | Line 1164: Selected work card |
| `public/images/projects/berserk-desktop.webp` | Berserk Tribute homepage | 1200×750 | Line 1173: Selected work card |
| `public/images/og-image.jpg` | Link preview card: name, title, headshot | 1200×630 | Lines 32 and 39: `og:image` and `twitter:image`, as `https://jjoshua.vercel.app/public/images/og-image.jpg` |
| `public/files/joshua-jalandoni-resume.pdf` | Public resume | — | Line 1082: "Resume ↗" button. **Missing, see TODO** |

Not files:

- **Favicon:** an inline SVG "JJ" monogram on line 26. There is no `favicon.ico` yet (see TODO).
- **Font:** Archivo from Google Fonts, line 45 (preconnects on lines 43–44). One variable
  family; the page requests five width/weight pairs: standard width at 400, 500, 600 and 700,
  and Expanded (125%) at 700 for the hero headline only. Google serves all five from a single
  file, about 88 KB for the Latin subset.

---

## In `public/` but not used on the site yet

| Path | What it is | Dimensions |
|---|---|---|
| `public/images/projects/rusty-mule-pizza-mobile.jpg` | Rusty Mule Pizza on a phone, top of page | 922×2048 |
| `public/images/projects/rubens-removal-mobile.jpg` | Rubens Removal on a phone, scrolled to a service card (see TODO) | 922×2048 |
| `public/images/projects/pinoy-eats-mobile.jpg` | Pinoy Eats on a phone, top of page | 922×2048 |
| `public/images/projects/mann-cayona-mobile.jpg` | Mann Cayona on a phone, scrolled to "The Weave" (see TODO) | 922×2048 |
| `public/images/projects/berserk-mobile.jpg` | Berserk Tribute on a phone, top of page | 922×2048 |
| `public/images/certifications/anthropic-claude-101.png` | Anthropic, "Claude 101" | 935×714 |
| `public/images/certifications/anthropic-claude-code-101.png` | Anthropic, "Claude Code 101" | 949×719 |
| `public/images/certifications/anthropic-claude-platform-101.png` | Anthropic, "Claude Platform 101" | 950×563 |
| `public/images/certifications/anthropic-claude-cowork-intro.png` | Anthropic, "Introduction to Claude Cowork" | 949×718 |
| `public/images/certifications/google-ai-professional-certificate.pdf` | Google AI Professional Certificate (Coursera, 7 courses) | PDF, 1 page |
| `public/images/clients/lion-sales-funnels.jpg` | Lion Sales Funnels logo | 200×200 |

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
| `_source/certificates/JoshuaJalandoni_AIFundamentals_Cert.pdf` | Original of `google-ai-professional-certificate.pdf` | PDF, 1 page |
| `_source/images/me.jpg` | Headshot, square crop | 400×400 |
| `_source/images/Screenshot 2026-09-11 175158.png` | Rubens Removal, mid-page section | 1887×891 |
| `_source/images/Screenshot 2026-09-11 175309.png` | Rusty Mule Pizza, "Friday Night Specials" section | 1615×890 |
| `_source/images/Screenshot 2026-09-11 175501.png` | Pinoy Eats, food photo carousel | 1852×828 |
| `_source/images/Google-Cloud-Logo.png` | Google Cloud logo | 3840×2160 |
| `_source/images/Logo_of_YouTube_(2015-2017).svg.webp` | YouTube logo, 2015–2017 version | 3840×1603 |

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

64 PNGs of the site taken during the redesign, in `before/`, `phase1/`, `phase2/`,
`foundation-before/`, and `foundation-after/`, at phone, tablet, and desktop widths. The two
`foundation-*` folders cover 360, 768, 1024, and 1440 in both themes, fold and full page, and
each holds a `metrics.json` with page height, heading sizes, and section gaps. Also excluded
from git by `.gitignore`.

---

## Outside this project

Files with personal data (IP address, earnings, account data, the full resume, personal
photos) are kept in `../jjoshua-private/`, outside this repository. They are not part of the
site.
