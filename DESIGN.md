# DESIGN.md

Design direction for **jjoshua.vercel.app** — the portfolio of Joshua Jalandoni.

This file is the source of truth for visual decisions. If code and this file disagree, this
file wins. If I change my mind, I update this file first.

---

## 1. Brief

**Subject.** A freelance web designer and developer in Bacolod City, Philippines, who builds
small sites for small businesses, plus a growing side in AI operations work.

**Audience.** Two groups, and they want different things:

- **Small business owners** — a pizzeria in Texas, a land-clearing company in Florida, a home
  kitchen, a painter. They are not technical. They are deciding whether to trust a stranger
  overseas with their business's front door. They want evidence of finished work and a
  process that feels safe.
- **AI ops / contract recruiters** — skimming for credentials, tools, and whether the work is
  real.

**The page's job.** Make a business owner think *this person is real, has done this before,
and will not waste my time.* Everything else is secondary.

**What is wrong with the current site.** Everything is set at display size, so nothing reads
as more important than anything else. Section spacing is arbitrary — some gaps reach
284px. The page has four sections where it needs nine. There is no evidence layer: no
logos, no stats, no experience, no certifications, no testimonials.

---

## 2. Principles

1. **Density over drama.** The fix for "looks fat" is more information at smaller sizes, not
   bigger type. Aim for roughly three times the current information per screen.
2. **Evidence beats adjectives.** Five real screenshots, twelve real certificates, and one
   real contract say more than any headline. Lead with artifacts.
3. **Spend boldness once.** One element on the page is allowed to be loud. Everything else
   stays quiet. Currently that element is the hero headline.
4. **Plain words.** The audience owns a pizzeria. Write the way you'd talk to them on the
   phone. No "leveraging," no "solutions," no "crafting digital experiences."
5. **Finished, not clever.** Every section fully built and responsive beats an ambitious
   section left half-done.

---

## 3. Typography

### Family

**Archivo** (Google Fonts, variable) — one family for the entire site, using its width and
weight axes instead of a second typeface.

- Display (hero headline only): `Archivo` at Expanded width (`font-stretch: 125%`), weight 700.
  Expanded is reserved for the hero so it stays the one loud element on the page.
- Section headings: `Archivo`, standard width, weight 700
- Body and UI: `Archivo`, standard width, weights 400 / 500 / 600

Load only these width and weight pairs. "Archivo Expanded" is not a separate Google Fonts
family; it is Archivo's width axis at 125%.

Rationale: the current site uses a very heavy grotesque, which is where "fat" comes from.
Archivo keeps that confident grotesque character but gets its impact from the *width* axis
rather than a Black weight, so headlines read as authoritative rather than bloated. Using one
variable family also keeps the font payload small.

Fallback stack: `'Archivo', 'Helvetica Neue', Arial, sans-serif`

### Scale

| Role | Size | Weight | Line height | Tracking |
|---|---|---|---|---|
| Hero | `clamp(2.25rem, 4.5vw, 3.5rem)` | 700 Expanded | 0.98 | -0.03em |
| Section heading | `clamp(1.9rem, 3vw, 2.6rem)` | 700 standard width | 1.05 | -0.02em |
| Card title | `1.25rem` | 600 | 1.25 | -0.01em |
| Body large | `1.0625rem` | 400 | 1.6 | 0 |
| Body | `1rem` | 400 | 1.6 | 0 |
| Small / meta | `0.875rem` | 500 | 1.45 | 0 |
| Label | `0.75rem` | 600 | 1.3 | 0.06em |

**Hard rule: the hero is the only thing on the page above 2.6rem.** No exceptions.

Body copy maxes at **68 characters** per line. Use `max-width: 34em`, not a pixel value.

### Section labels

Small labels above section headings, in sentence case with a short hairline rule to their
left — not tracked-out all caps. The hairline is drawn in `--muted`; `--line` is too faint to
carry the weight.

```
──  Selected work
    Sites that ship and get used.
```

Reason for the change: tracked-out ALL-CAPS eyebrows above every heading are the single most
common tell of a generated page right now. The label still does its structural job in
sentence case, and the hairline carries the visual weight instead of letterspacing.

---

## 4. Color

Nine tokens, each defined for both themes. Do not add a tenth without updating this file.

| Token | Dark | Light | Use |
|---|---|---|---|
| `--ink` | `#0E1116` | `#FBFBFC` | Page background |
| `--surface` | `#171B22` | `#FFFFFF` | Cards, raised panels |
| `--line` | `#262C36` | `#E3E6EB` | Borders, dividers, hairlines |
| `--text` | `#E9ECF1` | `#14181F` | Primary text |
| `--muted` | `#98A2B0` | `#5A6472` | Body copy, meta, labels |
| `--accent` | `#4F63E8` | `#3D4FD0` | Button fills, borders, focus rings. Never text. |
| `--accent-text` | `#7A8CF0` | `#3040B8` | Link text and any accent-colored text |
| `--on-accent` | `#FFFFFF` | `#FFFFFF` | Label text on `--accent` fills |
| `--signal` | `#E0A340` | `#9A6A12` | Available status, certification marks, highlights |

`--signal` in light mode sits at 4.57:1 against `--ink`. It passes, but with no margin. Never
lighten it. If it needs to change, darken it.

**On `--accent` and `--accent-text`:** restrict both to interactive elements only — links, the
primary button, the active nav state, and focus rings. It is currently applied to decoration
as well, which dilutes it. If it isn't clickable, it isn't blue.

`--accent` is for fills, borders, and focus rings only. On the dark ground it fails 4.5:1 as
text (3.86:1 on `--ink`), so any text that should read as accent — links, an active nav label —
uses `--accent-text` instead.

Labels on an `--accent` fill use `--on-accent`. Measured: 4.90:1 in dark, 6.51:1 in light.

**On `--signal`:** the amber gives the page a second voice so it doesn't read as the standard
near-black-plus-one-bright-accent layout. It also ties visually to the Rusty Mule gold and
the Pinoy Eats cream in the project screenshots. Use it sparingly: the availability dot, the
certification count, and nothing else at first.

**Light mode.** The theme toggle already exists. Every new section must work in both modes.
The light column above is a `[data-theme="light"]` override on the same token names — never
hardcode a color anywhere in the CSS.

---

## 5. Spacing

One scale. Every margin, padding, and gap on the site comes from it.

```css
--sp-0:  0.25rem;  /*  4px, tight UI only: chips, tags */
--sp-1:  0.5rem;   /*  8px */
--sp-2:  0.75rem;  /* 12px */
--sp-3:  1rem;     /* 16px */
--sp-4:  1.5rem;   /* 24px */
--sp-5:  2rem;     /* 32px */
--sp-6:  3rem;     /* 48px */
--sp-7:  4rem;     /* 64px */
--sp-8:  6rem;     /* 96px */
--sp-9:  8rem;     /* 128px */
```

- Section vertical padding: `--sp-7` (64px) on mobile, `--sp-8` (96px) on desktop. **Nothing
  larger.** Padding stacks where two sections meet, so the space between sections is 128px on
  mobile and 192px on desktop.
- Container: `max-width: 1180px` including side padding, side padding `--sp-4` mobile /
  `--sp-6` desktop.
- Grid gutter: `--sp-5`.
- Breakpoints: "mobile" is below 768px; desktop spacing starts at 768px. Multi-column layouts
  start at 1024px.

Radius: `--r-sm: 8px` (chips, buttons), `--r-md: 14px` (cards), `--r-lg: 20px` (large media).
Three values, chosen by element size — not one radius on everything.

---

## 6. Page structure

In order. Each section is one job.

| # | Section | Job | Priority |
|---|---|---|---|
| 1 | Nav | Wayfinding, sticky, scroll-spy | Must |
| 2 | Hero | Who, what, where, + stat strip | Must |
| 3 | Trust strip | Client logos | Must |
| 4 | Selected work | 5 project cards + filters | Must |
| 5 | Motion slot | Reserved — see §9 | Must (empty for now) |
| 6 | About | The person, + stats and capabilities in the right column | Must |
| 7 | Stack | Tools, grouped | Must |
| 8 | Experience | Timeline, numbered | Must |
| 9 | Certifications | 12 certificates, grouped by issuer | Must |
| 10 | Services | Three offers | Nice |
| 11 | Process | Four steps, numbered | Nice |
| 12 | Testimonials | Client quotes | Nice, pending content |
| 13 | Contact | Channels + availability | Must |
| 14 | Footer | Links, social, back to top | Must |

**On numbering:** use `01 / 02 / 03` markers only in **Experience** and **Process**, because
those are genuine sequences. Do not number the contact channels, the services, or the project
cards — a numbered list implies an order that isn't there.

### Section notes

**Nav.** Link only to sections that exist on the page. When a section is built, add its link in
the same change. Removing a link to a section that doesn't exist is a bug fix, not a copy
change.

**Hero.** Headline: three lines maximum at 1440, four at 360. The 360 limit applies after the
headline rewrite; the current headline runs six lines there. The headline column is at least
680px wide at 1440. Never shrink the hero below 2.25rem to hit a line count — the hero staying
the loud element matters more. Stat strip below the buttons — `4+ years`, `5 sites shipped`,
`12 certifications`, `2 client accounts` — with count-up on first view. Use the processed
headshot with the white background removed. File TBD. Fix the clipped project thumbnail behind
the portrait or remove it entirely.

**Trust strip.** Replace the five floating text names with a bordered strip of client logos.
Static row. No marquee — a scrolling logo band on a five-logo list is motion for its own sake.

**Selected work.** Card anatomy:

```
┌──────────────────────────────┐
│  [ screenshot, 16:10 ]       │
│                              │
│  Restaurant   Texas          │  ← tags
│  Rusty Mule Pizza            │  ← title
│  Two lines on what the       │
│  business needed and what    │  ← description
│  I built.                    │
│  HTML  CSS  JavaScript       │  ← tech chips
│  Visit site                  │  ← link
└──────────────────────────────┘
```

Filters above the grid: All / Restaurants / Service businesses / Creators.
Link text reads "Visit site" with the arrow as a separate `<span>` that animates on hover —
not an arrow character baked into the label.

**About.** The right half is currently empty. Fill it with a 2×2 stat grid and a short set of
capability chips. Body copy stays in the left column at 34em.

**Certifications.** Twelve uniform cards in a row is monotonous. Group them under two
subheads — Anthropic and Google — and let the Google one be visually larger since it's the
longer program.

**Contact.** Channel list, availability line, response time, location. No numbers.

---

## 7. Components

Build these once and reuse. Do not write bespoke markup per section.

- `.label` — section label with hairline
- `.section-head` — label + heading + optional deck
- `.btn` — variants `--primary`, `--secondary`, `--ghost`. The secondary button must carry its
  meaning in its label and text color, never in its border alone (`--line` is only 1.2–1.35:1
  against the background, which is right for a divider).
- `.card` — surface, border, radius
- `.tag` — category tag
- `.chip` — tech chip with optional icon
- `.stat` — number + caption, with count-up hook
- `.timeline-item` — numbered row for Experience

---

## 8. Motion

**One orchestrated moment, then nothing until the user acts.**

- **Page load:** the hero animates in once — headline, then subhead, then buttons, then the
  stat strip, staggered by about 80ms. This is the site's one non-interactive moment.
- **Stat count-up:** runs once when the strip first enters the viewport.
- **Everything else is user-triggered:** card hover, nav state, filter changes, focus rings.
  Keep these at 180–250ms with a standard ease.

**Do not add fade-and-slide-up reveals to every section on scroll.** I recommended this
earlier and I was wrong: scroll-triggered entrances on every section are the most recognizable
tell of a generated page, and on a page this long they make reading feel like it's fighting
back. One deliberate moment reads as designed; twelve read as a template.

`prefers-reduced-motion: reduce` disables the hero sequence and the count-up. Not optional.

---

## 9. Motion slot (reserved)

Section 5 is a reserved full-bleed band for a custom animation, currently unfinished.

Build it now as an empty, correctly-sized container:

```html
<section id="motion" class="motion-slot" data-motion-slot>
  <div class="motion-slot__frame" aria-hidden="true">
    <!-- Animation mounts here. Format TBD. -->
  </div>
</section>
```

- Aspect ratio 16:9, full-bleed (breaks the container), `max-height: 70vh`
- Placeholder: `--surface` fill with a hairline border. No "coming soon" text.
- Format not yet decided (MP4 / Lottie / canvas / CSS). Do not scaffold for a specific one.

---

## 10. Quality floor

Not negotiable, not features:

- Responsive at 360, 768, 1024, 1440
- Visible keyboard focus on every interactive element
- `prefers-reduced-motion` respected
- Alt text on every image
- Screenshots and photos in WebP; certificates and logos stay in their original format. All
  images sized to display dimensions, `loading="lazy"` below the fold
- Contrast: 4.5:1 body text, 3:1 large text, in **both** themes
- No layout shift on load — dimensions on every image

---

## 11. Things to avoid

Specific to this project, learned the hard way:

- Any type above 2.6rem outside the hero
- Section gaps outside the spacing scale
- Tracked-out all-caps labels above every heading
- `01 / 02 / 03` markers on content that isn't a sequence
- Meta strings joined with middle dots (`Texas · 2025 · Web`)
- Arrow characters (`→`) welded into link and button text
- The same border-radius and the same soft grey shadow on every element
- Identical rounded cards as the answer to every content type
- Scroll-reveal on every section
- Hardcoded hex values anywhere in the CSS
- Placeholder or invented copy — if content isn't ready, leave the section out

---

## 12. Open decisions

Tracked here so they don't get lost:

- [ ] Animation format and content
- [ ] Whether Services shows pricing
- [ ] Custom domain vs `.vercel.app`
- [ ] Case study pages for Rusty Mule and Rubens Removal
- [ ] Testimonials — requested from clients, none received yet
- [ ] Exact LSF job title and start date for the Experience entry
