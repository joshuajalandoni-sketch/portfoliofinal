# Portfolio design spec v2: jjoshua.vercel.app

This is the source of truth for the site's design. When code and this file disagree, this file wins. When this file is silent, choose the quieter, more restrained option.

Version 2 replaces the light-only minimal version. The goal is to move from "clean but plain" to "elevated and credible" while keeping what already works: the typography, the spacing discipline, and the hero work stack.

---

## 1. Direction

**Name:** Night studio

**In one sentence:** A dark, layered, proof-heavy portfolio where my face builds trust, my real client sites prove the work, and every section adds evidence that I'm the right person to hire.

### Principles

1. **Proof over promises.** Every section should add evidence: live sites, real numbers, tools, credentials, activity. Cut anything that is only decoration.
2. **One signature element.** The hero work stack is the memorable thing. Everything else supports it and stays disciplined.
3. **Depth through layers, not effects.** Depth comes from surfaces stepping up in lightness, hairline borders, and one soft glow. No neon, no heavy blur, no gradients on text.
4. **Real numbers only.** Never invent or round up a stat. If a number is small, show a different proof point instead.
5. **Borrow structure, never identity.** This design takes inspiration from the polish and density of modern developer portfolios (for example danielzanbaltazar.com). Do not copy any code, text, images, colors, or distinctive treatments from any reference site. Specifically: no yellow accent, no highlighter underline on the headline, no all-caps eyebrow labels, no line-grid background.

---

## 2. Design tokens

Dark is the default theme. Light is available through a toggle, and the light theme is essentially the v1 site.

### Dark theme (default)

| Token | Value | Use |
|---|---|---|
| `--bg` | `#0D0F13` | Page background |
| `--surface-1` | `#14171D` | Cards, chips |
| `--surface-2` | `#1B1F27` | Raised elements inside cards, hover states |
| `--border` | `rgba(255,255,255,0.08)` | Default hairline |
| `--border-strong` | `rgba(255,255,255,0.16)` | Hover and emphasis |
| `--text` | `#F2F3F5` | Headings and primary text |
| `--text-2` | `#9AA1AD` | Secondary text, second line of two-tone headings |
| `--text-3` | `#6B7280` | Captions and metadata |
| `--accent` | `#5B7CFF` | The only accent: primary buttons, links, focus rings, heatmap |
| `--accent-soft` | `rgba(91,124,255,0.14)` | Accent-tinted backgrounds and tags |
| `--available` | `#22C55E` | Availability dot only |

### Light theme

| Token | Value |
|---|---|
| `--bg` | `#FAFAF7` |
| `--surface-1` | `#FFFFFF` |
| `--surface-2` | `#F2F2EE` |
| `--border` | `#E4E4DE` |
| `--border-strong` | `#CFCFC7` |
| `--text` | `#1A1D24` |
| `--text-2` | `#5E6472` |
| `--text-3` | `#8A909B` |
| `--accent` | `#2F5BFF` |
| `--accent-soft` | `rgba(47,91,255,0.10)` |
| `--available` | `#1F9D55` |

Rules:
- One accent color. Never introduce a second one.
- Text on accent-filled buttons is white in both themes.
- Every token must work in both themes. Never hardcode a hex value in a component.

### Typography

- **Typeface:** Schibsted Grotesk for everything, weights 400, 500, and 700. Self-host it or use the framework's font loader with `font-display: swap`.
- **Scale:**
  - Hero headline: `clamp(44px, 6.4vw, 76px)`, weight 700, line-height 1.02, letter-spacing -0.035em
  - Section heading: `clamp(32px, 4vw, 48px)`, weight 700, line-height 1.08, letter-spacing -0.03em
  - Card title: 20px, weight 600 (or 700 if 600 isn't loaded)
  - Body: 17px, line-height 1.65
  - Small: 14px. Captions: 13px.
- **Two-tone headings:** the hero, section headings, and contact heading are two lines. Line 1 uses `--text`, line 2 uses `--text-2`. This is the main typographic device, so don't add other accents inside headings (no colored words, no underlines, no italics).
- **No eyebrow labels** above headings. No all-caps anywhere except official acronyms.
- Body text max width: 62ch.

### Shape and space

- Max content width: 1200px, side padding 24px (20px on mobile)
- Section spacing: 140px desktop, 88px mobile
- Radius: 20px cards, 16px images inside cards, 999px buttons, pills, and chips
- Borders: 1px `--border` on all cards. On hover, change to `--border-strong`. Project cards shift toward the accent at about 40% opacity.
- Shadows: dark theme uses none, because depth comes from surface steps. Light theme uses one soft shadow for floating chips and the work stack only.

### Texture and light

- **Dot texture:** a faint dot grid (1px dots, 24px spacing, about 6% opacity of `--text`) behind the hero only. Mask it with a radial fade so it disappears toward the edges.
- **Glow:** one soft radial glow in `--accent` at about 18% opacity, placed behind the work stack. It's the only glow on the page apart from a smaller one in the contact card.

### Motion

Motion is purposeful and limited:
1. **Page load (once):** the headline fades up, the photo appears, then the two screenshots slide out from behind the photo into their stacked positions. About 700ms total, ease-out.
2. **Work stack hover:** on desktop, the screenshots fan out slightly (rotate a few more degrees and translate outward). It feels like flipping through finished work.
3. **Client marquee:** a slow infinite scroll that pauses on hover.
4. **Card hover:** the border brightens and the image scales to 1.03. There is no card lift.
5. **Theme toggle:** a quick cross-fade of colors (150ms).

No scroll-triggered fade-ins on every section. No count-up animations on numbers. With `prefers-reduced-motion`, all motion is removed: the marquee becomes a static wrapped row and the stack appears in its final position.

---

## 3. Page structure (in order)

```
┌───────────────────────────────────────────────────────────────┐
│ Joshua Jalandoni   Work About Certifications Experience Contact [Let's talk] ◐ │  sticky, blurred
├───────────────────────────────────────────────────────────────┤
│ · · · · · · · · · · · · · · · · · · · · · · · · · · · · · ·    │
│  I design websites            ┌─────┐┌────────────┐   ◯ glow   │
│  that make small businesses   │shot ││   PHOTO    │[4+ yrs]    │
│  look legit.                  │shot ││  (front)   │            │
│  Subline                      └─────┘└────────────┘[12 certs]  │
│  [See my work] [Let's talk]                                   │
├───────────────────────────────────────────────────────────────┤
│ [ GitHub activity card: heatmap in blue ramp ]   (optional)   │
├───────────────────────────────────────────────────────────────┤
│ ← Rusty Mule · Rubens Removal · Pinoy Eats · Mann Cayona ... →│  marquee
├───────────────────────────────────────────────────────────────┤
│ Real sites for / real businesses.                              │
│ ┌──────────────── featured project (wide) ─────────────────┐  │
│ └──────────────────────────────────────────────────────────┘  │
│ ┌───────────┐ ┌───────────┐                                   │
│ └───────────┘ └───────────┘   2×2 grid                        │
│ ┌───────────┐ ┌───────────┐                                   │
│ └───────────┘ └───────────┘                                   │
├───────────────────────────────────────────────────────────────┤
│ What you get / when we work together.   [card][card][card]    │
├───────────────────────────────────────────────────────────────┤
│ Designer's eye / and an operator's discipline.                 │
│ About text + pills              [ profile card + stats ]      │
├───────────────────────────────────────────────────────────────┤
│ Certified in AI / by Anthropic and Google.                     │
│ [featured][featured][featured]   + compact list of the rest   │
├───────────────────────────────────────────────────────────────┤
│ My toolkit / from first sketch to live site.  icon tile grid  │
├───────────────────────────────────────────────────────────────┤
│ Where I've worked / and what I did there.   timeline          │
├───────────────────────────────────────────────────────────────┤
│ ┌─── Need a website? / Let's build it.  [Email] [Copy] ─────┐ │
│ └───────────────────────────────────────────────────────────┘ │
│ Footer                                                        │
└───────────────────────────────────────────────────────────────┘
```

### 3.1 Nav
- Sticky. Background is `--bg` at 72% opacity with `backdrop-filter: blur(12px)`, plus a bottom border that only appears after scrolling 8px.
- Left: "Joshua Jalandoni" (weight 600). No logo mark needed.
- Center/right: Work, About, Certifications, Experience, Contact. The active section is highlighted as you scroll.
- Right: "Let's talk" pill button (accent) and a theme toggle icon button (sun/moon, with an aria-label).
- The "Available for work" status moves into the hero chips so the nav stays clean.
- Mobile: name and menu button. The menu opens a full-width sheet with large links, and the CTA sits at the bottom.

### 3.2 Hero
- Two columns on desktop (text about 52%, stack about 48%). On mobile the stack comes first, scaled down, then the text.
- Headline, two-tone:
  - Line 1 (`--text`): "I design websites"
  - Line 2 (`--text-2`): "that make small businesses look legit."
- Subline: "Fast, clean sites for restaurants, service businesses, and creators. Designed, built, and launched from Bacolod City, Philippines."
- Buttons: "See my work" (accent pill, scrolls to Work) and "Let's talk" (outline pill, scrolls to Contact). Add a third outline button "Resume ↗" that opens `/public/resume.pdf` in a new tab (hide it if the file is missing).
- Availability line under the buttons: green dot + "Available for new projects".
- **Work stack (signature):** my photo `/public/me.jpg` in front in a 4:5 frame with 20px radius. The rusty-mule and rubens-removal screenshots sit behind it, offset left and rotated about -6° and 4°, with the accent glow behind them.
- **Floating chips (maximum two)** on the photo edges, using `--surface-1` at 85% opacity, a 1px border, and blur:
  - Top-left: "4+ years" / "building sites and automations"
  - Bottom-right: "12 certifications" / "Anthropic and Google" (links to the Certifications section)
  - These must stay true. Update them if the facts change.

### 3.3 GitHub activity (optional)
- A card showing my contribution heatmap for the last 12 months (username `joshuajalandoni-sketch`), with cells in a 5-step `--accent` ramp and empty cells in `--surface-2`.
- Header: GitHub icon, "GitHub activity", "[N] contributions in the last year", and a "View profile ↗" link.
- **Data:** fetch at build time or on the server with revalidation. If a token is needed, keep it in a server-only Vercel environment variable (`GITHUB_TOKEN`). Never ship it to the browser.
- **Show/hide rule:** controlled by a single config flag `SHOW_GITHUB_ACTIVITY`. If the fetch fails, the section is hidden entirely. It never shows an error or an empty grid. Only turn it on if the activity looks healthy, because a sparse heatmap is anti-proof.

### 3.4 Client marquee
- One line of small `--text-3` text above it: "Sites I've designed and built for".
- An infinite horizontal marquee of client wordmarks or logos in `/public/logos/` if present (grayscale, full color on hover), otherwise styled client names. Duplicate the list for a seamless loop and fade the edges with a mask.
- Pauses on hover. Static with reduced motion.

### 3.5 Work
- Heading: "Real sites for" / "real businesses."
- **Featured card (first project, full width):** screenshot on the left (about 60%) inside a minimal browser frame (three dots plus the domain in `--text-3`), and content on the right: tags, title, 2–3 sentence story (what they needed, what I built, the result), and "Visit site ↗" button.
- **Remaining four:** 2×2 grid. Each card has a browser-framed screenshot, tags, title, one-line description, and "Visit site ↗".
- **Tags:** small pills in `--accent-soft` with `--accent` text, sentence case, max 3 per card. Use a category tag (Restaurant, Service business, Personal project) plus tech tags only if accurate.
- No filter tabs until there are 9 or more projects.

| Project | Category tag | Description |
|---|---|---|
| Rusty Mule Pizza (featured) | Restaurant | A wood-fired pizzeria in Karnack, Texas that needed its menu, hours, and phone orders in one place. |
| Rubens Removal LLC | Service business | A Florida land-clearing company that needed local visitors to turn into quote requests and calls. |
| Pinoy Eats | Restaurant | Keep the existing description. |
| Mann Cayona | Keep existing | Keep the existing description. |
| Berserk | Personal project | A dark, atmospheric tribute site built to push layout and mood further than client work allows. |

### 3.6 What you get (services)
- Heading: "What you get" / "when we work together."
- Three cards in a row: a small outline icon (24px, `--text-2`), title, and description. Keep the existing copy for Website design, Build and launch, and Automation.

### 3.7 About
- Heading: "Designer's eye" / "and an operator's discipline."
- **Left column:** keep my existing About paragraphs. Below them, specialty pills (outline, sentence case): Website design, Landing pages, Web development, Automation, AI workflows.
- **Right column: profile card** (`--surface-1`, 20px radius):
  - Top: candid photo `/public/me-candid.jpg` (falls back to `me.jpg`), name, "Web designer and developer · Bacolod City, PH"
  - A 2×2 stat grid with hairline dividers, using real values only: **4+** Years building · **[N]** Sites launched · **12** Certifications · **GMT+8** Time zone
  - A full-width "Start a project" accent button that scrolls to Contact, with a smaller "Resume ↗" text link under it
- This fills the empty right half the v1 About section had.

### 3.8 Certifications
- Heading: "Certified in AI" / "by Anthropic and Google."
- Summary line under the heading, with one small check icon: "12 certifications, each with a public verification link." Keep this count in sync with the data file automatically.
- **Featured row (3 cards):** certificate thumbnail from `/public/certificates/` (16:10 crop with 12px radius and a hairline border), issuer icon and name, credential title, issued date, and a "Verify ↗" link. Clicking the thumbnail opens a lightbox with the full certificate.
- **Everything else: compact list** in two columns (one on mobile), grouped under small `--text-3` group names ("Claude and the Anthropic platform", "AI Fluency"). Each row has the title, "Issuer · Month Year" in `--text-3`, and "Verify ↗" aligned right, separated by hairlines. No thumbnails and no badges in the list.
- **Lightbox:** an accessible dialog with focus moved in and returned on close; closes with Esc, the close button, or a backdrop click; uses the optimized full-size image.
- **Data-driven:** all certificates live in one data file (for example `content/certifications.ts` or `.json`) with `id`, `title`, `issuer`, `group`, `issued` (YYYY-MM), `verifyUrl`, `image`, `featured`, and `order`. Adding a certificate later means adding one entry, not editing components.
- **Rules:** one entry per real credential. A verification link is a button on its credential, never its own card. The resume is not a certificate. It lives in the hero and About card. No "VERIFIED" badge repeated on every item; the summary line covers it once.

| Order | File name in `/public/certificates/` | Title | Issuer | Group | Issued | Featured |
|---|---|---|---|---|---|---|
| 1 | `google-ai-professional` | Google AI Professional Certificate (7 courses) | Google · Coursera | — | Jun 2026 | Yes |
| 2 | `anthropic-ai-fluency-framework` | AI Fluency: Framework and Foundations | Anthropic | AI Fluency | TODO | Yes |
| 3 | `anthropic-claude-code-101` | Claude Code 101 | Anthropic | Claude | TODO | Yes |
| 4 | `anthropic-claude-platform-101` | Claude Platform 101 | Anthropic | Claude | TODO | |
| 5 | `anthropic-claude-101` | Claude 101 | Anthropic | Claude | TODO | |
| 6 | `anthropic-intro-claude-cowork` | Introduction to Claude Cowork | Anthropic | Claude | TODO | |
| 7 | `anthropic-ai-fluency-builders` | AI Fluency for Builders | Anthropic | AI Fluency | Jul 2026 | |
| 8 | `anthropic-ai-fluency-small-businesses` | AI Fluency for Small Businesses | Anthropic | AI Fluency | Jul 2026 | |
| 9 | `anthropic-ai-capabilities-limitations` | AI Capabilities and Limitations | Anthropic | AI Fluency | Jul 2026 | |
| 10 | `anthropic-ai-fluency-nonprofits` | AI Fluency for Nonprofits | Anthropic | AI Fluency | Jul 2026 | |
| 11 | `anthropic-ai-fluency-educators` | AI Fluency for Educators | Anthropic | AI Fluency | Jul 2026 | |
| 12 | `anthropic-ai-fluency-students` | AI Fluency for Students | Anthropic | AI Fluency | Jul 2026 | |

- File names can end in `.png`, `.jpg`, or `.pdf`. For PDFs, render the first page to an image once during setup and commit the optimized result.
- Verify URLs: reuse the ones already in my codebase if they exist (Coursera and verify.skilljar.com links). Anything missing is a `TODO` for me. Never guess a URL.

### 3.9 Toolkit
- Heading: "My toolkit" / "from first sketch to live site."
- Grouped rows with a small group name (sentence case, `--text-3`) and a thin rule: Design, Build, Deploy, AI and automation.
- Square tiles (about 104px, `--surface-1`, 16px radius) with a brand icon (Simple Icons) and a name. Icons are monochrome `--text-2` by default and turn brand-colored on hover, which distinguishes the grid from a plain colorful logo wall.
- **Only list tools I actually use.** Confirmed: Figma, Claude Code, GitHub, Vercel. Add others only after I confirm them.

### 3.10 Experience
- Heading: "Where I've worked" / "and what I did there."
- A single-column timeline (max width about 760px): a vertical hairline with dots. Each entry has role, organization, dates, and one line about the work. The current role gets a small green "Now" pill.
- Use placeholder entries marked `TODO` for me to fill in. Only list employers and clients I'm allowed to name publicly.

### 3.11 Contact
- A large card (`--surface-1`, 24px radius) with a soft accent glow in one corner.
- Heading: "Need a website?" / "Let's build it."
- Body: "Tell me about your business and what you need it to do. I reply to every message, usually within a day."
- Actions: "Email me" (accent pill, mailto) and a "Copy email" icon button that shows a "Copied" confirmation for 2 seconds.
- Social row as icon + label buttons: LinkedIn, GitHub, YouTube, Facebook (use the existing links).
- Small line: "Based in Bacolod City, Philippines · GMT+8 · Working with clients worldwide".

### 3.12 Footer
- Name and year on the left. Social icons and "Back to top ↑" on the right. `--text-3`, 14px.

---

## 4. Theme toggle
- Dark by default for first-time visitors. The choice is remembered in `localStorage`.
- Apply the saved theme with a tiny inline script in `<head>` before first paint so there is no flash of the wrong theme.
- The toggle has an aria-label that updates ("Switch to light theme" / "Switch to dark theme").

---

## 5. Assets

```
public/
├── me.jpg                 hero headshot (existing)
├── me-candid.jpg          NEW: casual photo for the About card
├── resume.pdf             my resume (hero button + About card link)
├── certificates/          one file per certificate, named as in section 3.8
├── logos/                 optional: client logos (svg or png, transparent)
└── work/
    ├── rusty-mule.jpg
    ├── rubens-removal.jpg
    ├── pinoy-eats.jpg
    ├── mann-cayona.jpg
    └── berserk.jpg
```

- Generate optimized AVIF/WebP versions with explicit width and height. Hero images load eagerly with high priority. Everything else is lazy-loaded.
- Generate `og.png` (1200×630) on the dark theme: headshot, name, and "Web designer and developer".
- Favicon set: a "JJ" monogram in `--accent` on `--bg`, as SVG plus a PNG fallback and an Apple touch icon.

---

## 6. Technical and deployment requirements

- Real, server-rendered or static HTML on first load. No loading screen, no "Unpacking..." state.
- **SEO:** unique `<title>` and meta description, canonical URL, Open Graph and Twitter tags, `sitemap.xml`, `robots.txt`, and JSON-LD `Person` schema (name, job title, URL, sameAs social links).
- **Performance:** Lighthouse mobile scores of at least 90 for Performance and 95 for Accessibility, Best Practices, and SEO. LCP under 2.5s, CLS under 0.05. No heavy libraries (no three.js, no large animation frameworks). CSS transitions and small vanilla JS are enough.
- **Accessibility:** semantic landmarks, one `<h1>`, visible focus rings in `--accent`, alt text on every image, contrast of at least 4.5:1 in both themes, full keyboard support for the menu and theme toggle, and the marquee duplicate hidden from screen readers.
- **Responsive:** check at 375, 768, 1024, 1440, and 1920px.
- **Deployment (Vercel):** work on a branch. Each push to that branch gets a Vercel preview URL for review. Merge to main only after approval. Secrets live only in Vercel environment variables, never in the repo or client bundle.

---

## 7. Don'ts

- No copying code, copy, images, colors, or signature treatments from any reference site
- No yellow, and no second accent color
- No highlighter, underline, colored word, or italic word inside headlines
- No all-caps eyebrow labels
- No invented or inflated numbers
- No filter tabs with fewer than 9 projects
- No scroll fade-ins on every section, no count-up numbers, no cursor effects, no particle backgrounds
- No more than two floating chips in the hero
- No duplicate certificate entries, no resume inside the certificate grid, and no "verified" badge repeated on every item
- No loading screen

---

## 8. Before shipping

- [ ] `me-candid.jpg` added (or I accept the headshot fallback)
- [ ] Stats in hero chips and the About card are true
- [ ] Toolkit only shows tools I use
- [ ] Experience timeline `TODO` entries filled in or removed
- [ ] Every certificate has the right date, image, and a working verify link
- [ ] GitHub activity looks healthy, or `SHOW_GITHUB_ACTIVITY` is off
- [ ] Both themes checked on phone and desktop
- [ ] Link preview shows the OG image on Messenger and LinkedIn
- [ ] Lighthouse targets met on the Vercel preview URL
