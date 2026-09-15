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
| Hero | `clamp(2.25rem, 4vw, 3.125rem)` | 700 Expanded | 0.98 | -0.03em |
| Section heading | `clamp(1.75rem, 2.7vw, 2.375rem)` | 700 standard width | 1.05 | -0.02em |
| Row title (`--fs-row`) | `1.5rem` | 600 | 1.25 | -0.01em |
| Card title | `1.15rem` | 600 | 1.25 | -0.01em |
| Body large | `1rem` | 400 | 1.6 | 0 |
| Body | `0.9375rem` | 400 | 1.6 | 0 |
| Small / meta | `0.8125rem` | 500 | 1.45 | 0 |
| Label | `0.75rem` | 600 | 1.3 | 0.06em |

The scale was brought down about 8% because everything read too large. Two sizes deliberately
didn't move: the hero keeps its 2.25rem floor (on a phone the smaller size saved no line, and
the hero staying the loudest element matters more), and the label stays at 0.75rem, the smallest
size on the page. At 0.6875rem (11px) labels, tech chips, and the "Verify" link read too small.

The row title is for project names in the desktop Selected work list (§6). It sits between card
title and section heading so a list of names never reads as a list of headings: at the section
heading size, the "Selected work" heading looked like a sixth row. It borrows the card title's
weight, line height, and tracking.

**Hard rule: the hero is the only thing on the page above 2.375rem.** No exceptions.

Body copy maxes at **68 characters** per line. Use `max-width: 34em`, not a pixel value.

### Section labels

Small labels above section headings, in sentence case with a small monitor icon to their left —
not tracked-out all caps. Every label on the page takes the icon; none keeps the old hairline
rule. The icon is an outlined monitor (a screen and a stand) drawn for this site, inline SVG from
the page's icon sprite, stroked in `currentColor` so it takes the label's `--muted` (7.38:1 on
`--ink` in dark, 5.95:1 in light, above the 3:1 bar for graphics). It sits `--sp-2` from the text,
the gap the hairline had, and is centered on the label's height, not its baseline.

```css
--icon-label: 14px;  /* the label icon, square */
```

```
[▭]  Selected work
     Sites that ship and get used.
```

Reason for the change: tracked-out ALL-CAPS eyebrows above every heading are the single most
common tell of a generated page right now. The label still does its structural job in
sentence case, and the icon carries the visual weight instead of letterspacing.

---

## 4. Color

Nine tokens, each defined for both themes. Do not add a tenth without updating this file.

Sage and bone. The whole palette is warm: the dark background is a warm near-black with a green
cast, not a neutral grey, and text is bone, not pure white.

| Token | Dark | Light | Use |
|---|---|---|---|
| `--ink` | `#171A15` | `#F7F6F1` | Page background |
| `--surface` | `#1F2320` | `#FFFFFF` | Cards, raised panels |
| `--line` | `#2E332B` | `#E2E0D7` | Borders, dividers, hairlines |
| `--text` | `#F2EFE8` | `#1B1E18` | Primary text |
| `--muted` | `#A8A99C` | `#5C6055` | Body copy, meta, labels |
| `--accent` | `#8FA876` | `#5A7042` | Button fills, borders, focus rings. Never text. |
| `--accent-text` | `#A3BC8A` | `#47592F` | Link text and any accent-colored text |
| `--on-accent` | `#171A15` | `#FFFFFF` | Label text on `--accent` fills |
| `--signal` | `#C9C2B0` | `#6E6A5C` | The availability dot and the certification count |

**Measured contrast** for every pairing the CSS uses. The bar is 4.5:1 for text, and 3:1 for
large text and for focus rings and fills, in both themes.

| Pair | Needs | Dark | Light |
|---|---|---|---|
| `--text` on `--ink` | 4.5 | 15.30 | 15.58 |
| `--text` on `--surface` | 4.5 | 13.86 | 16.86 |
| `--muted` on `--ink` | 4.5 | 7.38 | 5.95 |
| `--muted` on `--surface` | 4.5 | 6.68 | 6.44 |
| `--accent-text` on `--ink` (links, active nav) | 4.5 | 8.47 | 7.09 |
| `--accent-text` on `--surface` ("Verify" on cards) | 4.5 | 7.67 | 7.67 |
| `--accent-text` on the ghost button's hover fill | 4.5 | 7.00 | 6.08 |
| `--on-accent` on `--accent` | 4.5 | 6.72 | 5.48 |
| `--on-accent` on `--accent` at the primary button's hover (`brightness(0.9)`) | 4.5 | 5.50 | 6.41 |
| `--signal` on `--ink` (certification count, large) | 3 | 9.90 | 5.00 |
| `--accent` on `--ink` (focus rings, fills) | 3 | 6.72 | 5.07 |
| `--accent` on `--surface` (focus rings on cards) | 3 | 6.09 | 5.48 |
| `--signal` on `--ink` (availability dot) | 3 | 9.90 | 5.00 |

For reference, with no bar to meet: `--line` is 1.36:1 on `--ink` and 1.23:1 on `--surface` in
dark, 1.22:1 and 1.32:1 in light. The marquee logos (`--muted` at 55%) are 3.15:1 in dark and
2.33:1 in light.

**On `--accent` and `--accent-text`:** restrict both to interactive elements only — links, the
primary button, the active nav state, and focus rings. If it isn't clickable, it isn't
accent-colored. One recorded exception: the GitHub graph (§6) is a third-party image drawn in
the light `--accent`, since the service takes one color for its squares.

`--accent` is for fills, borders, and focus rings only; text that should read as accent — links,
an active nav label — uses `--accent-text`. In this palette `--accent` would pass as text (6.72:1
in dark, 5.07:1 in light), but the roles stay separate, so either token can change without
breaking the other.

Labels on an `--accent` fill use `--on-accent`. In dark that's a dark label, the `--ink` value:
white on the light sage fill is only 2.62:1.

**On `--signal`:** a bone tone for status and a few highlights: the availability dot and the
certification count. It's never a link color; links use `--accent-text`. It sits close to
`--muted` (1.34:1 apart in dark, 1.19:1 in light), so it reads as a quiet highlight, not a
second color.

Colors that can't read a token are copied from one, and change with it: the address-bar color
(`theme-color`, the dark `--ink`, which the script then keeps in sync), the favicon (dark `--ink`
ground, dark `--text` letters), the GitHub graph's URL (light `--accent`), and the link preview
image, `og-image.jpg` (the light tokens).

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
- Breakpoints: "mobile" is below 768px; desktop spacing starts at 768px. Two-column grids may
  start at 768px; three or more columns, and side-by-side layouts like the hero, start at
  1024px.
- Exception: small repeated items (tool tiles) aren't content columns, so
  they may run two across on phones and four across from 768px. Tool tiles go on to five at
  1024px and six from 1180px, the container's width.

Radius: `--r-sm: 8px` (chips, buttons), `--r-md: 14px` (cards), `--r-lg: 20px` (large media).
Three values, chosen by element size — not one radius on everything.

---

## 6. Page structure

In order. Each section is one job.

| # | Section | Job | Priority |
|---|---|---|---|
| 1 | Nav | Wayfinding, sticky, scroll-spy | Must |
| 2 | Hero | Who, what, where, + stat strip | Must |
| 3 | Tools marquee | GitHub graph, then tools and platforms I work with | Must |
| 4 | Selected work | 4 client case-study cards + filters, then a Personal projects line | Must |
| 5 | Motion slot | Reserved — see §9 | Must (empty for now) |
| 6 | About | The person, + stats and capabilities in the right column | Must |
| 7 | Stack | Tools, grouped | Must |
| 8 | Experience | Timeline | Must |
| 9 | Brands | Companies Joshua worked for or with, one logo each | Nice, pending logos |
| 10 | Certifications | 12 certificates, grouped by issuer | Must |
| 11 | Services | Four offers | Nice |
| 12 | Process | Four steps, numbered | Nice |
| 13 | Testimonials | Client quotes, under their project in Selected work (not a section) | Nice, one so far |
| 14 | Contact | Channels + availability | Must |
| 15 | Footer | Links, social, back to top | Must |

**On numbering:** use `01 / 02 / 03` markers only in **Process**, because it's a genuine
sequence. Do not number the contact channels, the services, or the project
cards — a numbered list implies an order that isn't there.

### Section notes

**Nav.** Link only to sections that exist on the page. When a section is built, add its link in
the same change. Removing a link to a section that doesn't exist is a bug fix, not a copy
change. Links follow page order. Below 1024px they live in the menu. At 1024px the seven links,
the CTA, and the theme toggle fit with 62px to spare; an eighth link needs re-measuring.

**Hero.** Headline: "Websites and automations for small businesses." Two tones, each half
starting its own line: "Websites and automations" in `--text`, "for small businesses." in
`--muted`. Three lines maximum at 1440, four at 360; measured, it runs exactly three and four.
The headline column is at least 680px wide at 1440. Never shrink the hero below 2.25rem to hit a
line count — the hero staying the loud element matters more. Stat strip below the buttons, with
count-up on first view, captions from CONTENT.md: `4+` years building, `4` client sites shipped,
`12` certificates earned. The numbers are compact (`.stat--compact`) so the headline stays the
loud element. The portrait is a photo of Joshua at his desk (`joshua-at-desk.webp`), cropped to
the photo box's 4:5 with his face in the upper part of the frame (eyes at 44%, head center at
41%) and the monitor, PC, keyboard, and part of the laptop still in view, so it shows the person
and where the work happens. Nothing is added on top of it: no floating badges and no project
screenshots. The screens in the photo are unreadable, and must stay that way in any retake (no
client work on show, CLAUDE.md). Exported at 2x its largest rendered size (368×460 from 1024px),
so 736×920. Capped at 12rem wide below 1024px so the headline shows on a phone's first screen.

**GitHub graph.** Joshua's GitHub contribution graph, directly above the tools marquee in the
same band, with a hairline rule between them. Supporting detail, not its own section, and not in
the nav. Labeled "GitHub" (`.label`), never "Recent activity": the graph has had blank weeks at its
right edge, and the label must not claim what the graph doesn't show. No contribution count. The
GitHub mark (Octicons `mark-github-16`) sits before the word in the label's color, 16px
(`--icon-sm`), `--sp-1` from the word and `--sp-2` after the label's monitor icon. The image comes from
ghchart.rshah.org in the light `--accent`, `#5A7042` (the URL can't read a token, so it changes
with the token), with a "View GitHub profile" link below it that opens in a new tab. The dark
`--accent`, `#8FA876`, doesn't work: the service shades lighter from the color it's given, and
from that light sage its quietest days match the empty squares (1.01:1 in light, 1.04:1 in dark). The graph box keeps the image's 663:104 shape at a fixed 765 × 120px and is sized before the
image loads, so nothing moves. The label, graph, and link are centered in the container as one
group, with the label and link on the graph's left edge. At 1440 the group starts 159.5px in from
the Tools label below it; that offset is deliberate. Where the container is narrower than the
graph, the page never scrolls sideways: the graph scrolls inside its own box, which opens at the
newest weeks and can be reached by keyboard while it scrolls.
It's a third-party service and can go down, so if the image fails to load the whole block hides —
label, graph, and link — because a broken image is worse than no graph. The hide needs JavaScript,
so without it the block is hidden, like the marquee. The service can't tell an empty or stale
graph from a good one, and neither can the hide.

The service draws empty squares in a fixed `#EEEEEE` whatever color it's given, which is 15.15:1
on the dark `--ink`, brighter than anything else on the page. In the dark theme the image is
inverted most of the way (`invert(0.85) hue-rotate(180deg)`). Measured on `--ink`, from the
rendered pixels: empty squares 1.37:1, labels 4.83:1, filled squares 2.58–6.61:1 (1.88–4.82:1
against the empty ones), with the busiest days brightest, as on GitHub's own dark theme. Dimming
with brightness alone doesn't work: the filled squares are darker than the empty ones, so they
vanish first. When this was tuned, on the earlier indigo palette, the brightness that dimmed the
empty squares to 1.64:1 took the busiest days to 1.04:1, where they read as holes. The light theme
uses no filter: empty squares 1.07:1, labels 4.20:1, filled squares 1.88–6.96:1 (1.75–6.49:1
against the empty ones).

**Tools marquee.** Labeled "Tools and platforms I work with", between the hero and Selected work,
as a supporting band with no section padding of its own. These are tools Joshua uses, not clients
or endorsements: the label never reads "Trusted by", and no logo is added beyond the approved list.
(It replaced a "Selected clients" strip, which repeated the client names already on the Selected
work cards.) One-color marks from the Stack icon sprite, in `--muted` at 55% opacity, about 28px
(`--band-logo-h`, shared with the brands band)
and sized by eye: each mark gets the same visual area rather than the same box. A continuous
horizontal scroll, one loop in about 40s; the set is drawn twice for a seamless loop, the copy
hidden from screen readers, and both edges fade out. No hover state: the logos aren't links, and
they're a list of tools rather than something to inspect (§11). A visible pause/play button,
because motion that runs longer than five seconds must be stoppable (WCAG 2.2.2) and hover does
nothing on a touch screen. Under `prefers-reduced-motion`, nothing moves: the logos sit in one
static, centered, wrapped row and the button is hidden.

**Exception to "no marquee":** this is the only element on the page that moves on its own. It's
allowed because the list is long enough to scroll without the same logo showing twice on screen
(the set is wider than the 1,084px strip at 1440), it stays quiet (muted, 55% opacity), and the
pause button and the reduced-motion row mean no one has to watch it move.

**Selected work.** Two layouts from the same data, chosen by the visitor's device.

- **Cards** are the default: every phone, every tablet, every touch screen at any width, and any
  screen narrower than 1024px. The screenshot is always visible. This isn't a fallback; it's
  what most visitors see.
- **A list with a hover preview** appears only on a screen at least 1024px wide with a mouse or
  trackpad (`(min-width: 1024px) and (hover: hover) and (pointer: fine)`).

The reason for two: on a wide screen with a mouse, a list shows all four projects at a glance
and still gives each screenshot on demand. On touch there's no hover, and a screenshot hidden
behind an interaction that doesn't exist is a screenshot nobody sees. The gate is the pointer,
not width alone: an iPad in landscape is 1024–1366px wide and can't hover, so it keeps the cards.
Width still counts too: a narrow browser window with a mouse gets cards, because the list needs
the room. Evidence beats adjectives (§2), so neither layout drops information: the list moves
the screenshot into the preview and keeps everything else.

Card anatomy:

```
┌──────────────────────────────┐
│  [ screenshot, 16:10 ]       │
│                              │
│  Restaurants                 │  ← category tag
│  Rusty Mule Pizza            │  ← title
│  Problem: Every order came   │
│  in by phone. …              │
│  What I built: A one-page    │  ← case study, three labeled lines
│  site with the menu, …       │
│  Result: Customers can see … │
│  React  Vite                 │  ← tech chips
│  Visit site                  │  ← link
└──────────────────────────────┘
```

Every client project is a case study: three labeled lines, Problem, What I built, and Result, in
that order, on the card and in the list alike. Each label runs in at the start of its line in
`--text` at the semibold weight (`--fw-semibold`, the heaviest body weight in §3), and the text
stays `--muted` at the body size, so the labels stand out through weight and color, not size.
Lines sit `--sp-1` apart, at the body measure. The copy is in CONTENT.md.

One tag: the category, plural, exactly as the filter names it. No location tag, and no year: the
year is in the list only. Tech chips list what the live site is actually built with. Link text
reads "Visit site" with the arrow as a separate `<span>` that animates on hover — not an arrow
character baked into the label. From 768px, the site's phone screenshot overlaps the lower-right
corner of the desktop screenshot. Below 768px only the first three matching cards show, with a
"Show all projects" button (`.btn--secondary`) that reveals the rest in one step, the same
pattern as Certifications.

List row anatomy:

```
──────────────────────────────────────────────────────────────────────────────
Rusty Mule Pizza                         [ preview column ]    Restaurants  2025
Problem: Every order came in by phone.                               React  Vite
What I built: A one-page site with the…
Result: Customers can see the menu and…
──────────────────────────────────────────────────────────────────────────────
```

The name is in `--fs-row` (§3), the case study below it at the body measure, and category, year,
and tech chips on the right, with hairline rules between rows. The whole row links to the live
site (a new tab): the name is the link, and its overlay covers the row. The case study wraps
rather than being cut short: it's the evidence.

The middle column of every row is kept empty, 380px wide (`--work-preview-w`). Pointing at a row
shows that project's desktop screenshot in a floating preview, 380px wide, that follows the
cursor with a slight lag. Keyboard focus shows the same preview, held still in the row's empty
middle column and centered on the row. The column exists so the still preview never covers the
row's own text: with descriptions and chips in the row, the widest natural gap is 183px at 1024
and 354px from 1280, never the 380px the preview needs.
The preview fades in and out over 180ms (`--dur-fast`). Under reduced motion it doesn't follow or
fade: it appears at once, beside the row, whether the row was pointed at or focused. While a
preview shows, the other rows' names go to `--muted` and the active row's name stays `--text`.
The preview is fixed-position and moved with `transform`, kept inside the window and below the
nav, so it never pushes content or causes scrolling. Its four images load after the page has
loaded, and only where the list shows, so the first hover isn't blank and touch screens never
download them.

Filters above both layouts: All / Restaurants / Service businesses / Creators, one tab per client
category. They filter the list and the cards together. Filtering is instant, with no animation,
and a filtered view is linkable (`#work/restaurants`). A link to a tab that doesn't exist, such as
the old `#work/personal`, shows All. The selected filter is an `--accent` fill. Below 768px the
filters are one row that scrolls sideways.

**Testimonials** go under the project they're about, not in a section of their own: a client's
words next to the work they describe are evidence (§2). A project's optional `testimonial` in the
data renders a `.testimonial` under its card (`--sp-3` below it) and under the case study in its
list row, so adding one never changes the markup. Plain text in site type: the quote in `--text`
at the body size, in typographic quotation marks, then "— source, detail" in `--muted`, small, the
source's name linking to the project's live site (a new tab). No card, border, quote-mark graphic,
or avatar. Each project spans two rows of the card grid (a subgrid): the card, then the box under
it. Cards in a row keep one height whether or not one has a testimonial, projects stay `--sp-6`
apart, and the grid pulls up by that `--sp-6` at its end so what follows doesn't move.

**Personal projects** (Berserk Tribute) aren't client work, so they sit outside the list, the
cards, and the filters: a `.label` "Personal projects" below the grid, then each project's name
as a link to the live site (a new tab), with its short description beneath in `--muted` at the
body measure. It takes the title size and internal spacing of the client projects shown above
it, so it reads as a project, but never a card border or surface. With the cards: the name at
card-title size (`--fs-h3`), a card body's `--sp-4` padding, `--sp-2` between label, name, and
description, and `--sp-6` below the grid. With the list: the name at `--fs-row`, a row's `--sp-5`
above and below with no side padding, so it lines up with the row names, and `--sp-1` from name
to description. No screenshot and no hover preview (its data carries no screenshots), no case
study, no tech chips. Hidden when there are none.

**About.** Body copy in the left column at 34em. The right column opens with Joshua's
illustration (`jj-illustration.webp`), 200px tall (`--about-illustration-h`), uncropped and in its
own colors; at 1440 it makes the side column 445px against the copy's 448px. It's black lines with
nothing filled between them, so on the dark page alone the lines are about 1.03:1: it sits on a
light tile (`.about__illustration`: `--illustration-ground`, `--sp-3` padding, `--r-lg`), which is
the bone `--text` in dark and the white `--surface` in light, an alias rather than a tenth color.
Below 1024px the columns stack and it falls between the copy and the pull quote. Then a pull quote
(`.pull-quote`: card-title size in `--text`, hairline rule above), then the capability chips:
Websites, Landing pages, Automations, Redesigns, Data annotation, Quality review, Community
management. These are services, so they belong here rather than in Stack. No stat grid here:
the hero strip already shows those numbers, and repeating them two screens later adds nothing.

**Experience.** A timeline of seven entries, newest first, matching the resume. Role as the
title; organization and dates as separate meta tags, and an entry with no named organization
shows its dates alone. Below 768px only the first three show, with a "Show
full history" button (`.btn--secondary`) that reveals the rest in one step, the same pattern as
Selected work. An entry can carry a client review under its description (`.testimonial--quiet`,
`--sp-2` below it): smaller than the description (`--fs-small` against the body size) and all in
`--muted`, which is the quietest text token that still passes 4.5:1 in both themes, so the review
steps back by size rather than by a fainter color. Words and source only: never a star rating,
rate, or hours.

Each entry's company and dates line starts with a mark, centered on the line, `--sp-2` from the
text. A company entry shows its logo from `public/logos/`, sized optically rather than to one
height. One height failed: a wide wordmark at 24px has letters too small to read, while square
marks looked right. Each logo fits the box for its kind, a max width and a max height, so a
square mark stops at the height and a wide one at the width:

```css
--logo-mark-max-w: 44px;      /* marks: square, tall, or icon-like (Roblox, Lion Sales Funnels, */
--logo-mark-max-h: 22px;      /*   VA House PH, the American Express box) */
--logo-wordmark-max-w: 80px;  /* wordmarks: mostly lettering (Capital One), which needs height */
--logo-wordmark-max-h: 28px;  /*   to read; about the company name's width, so it doesn't overpower it */
```

Rendered: Roblox and American Express 22×22, Lion Sales Funnels 16×22, VA House PH 44×21, Capital
One 78×28 (its capitals 11.3px, a little taller than the 13px company name's). The data marks a
logo `kind: 'wordmark'`; the height is worked out from the file's shape, so the box is sized
before the image loads. The American Express file is a square box, so it's a mark: its lettering
is 15.7% of the box's height, about 3.5px at 22px, and can't be read at any size that fits the
line. Logos rest in grayscale at 60% opacity (`--timeline-logo-opacity`) and go to full color on
hover over `--dur-fast`, an exception to §11 like the brand logos. Freelance work has no company,
so it shows the section-label monitor at a mark's height (`--logo-mark-max-h`), in `--muted`, never
grayed or faded; Digital Engagement & Operations Strategist names no employer and shows no mark.

The logos were supplied by Joshua in September 2026. This spec earlier kept the Roblox and American
Express marks off the page for lack of trademark permission; permission for every logo here is
tracked in §12 and should be settled before deploy. Two files barely show on the dark page: the
Capital One wordmark is dark navy (median 1.2:1 at rest, 1.52:1 even in full color) and VA House's
middle stroke is black (1.44:1 at rest). Reversed, light versions of those two files are wanted.

**Brands.** After Experience, labeled "Brands I've worked with", as a supporting band with no
section padding of its own. A static, centered, wrapped row of one-color logos in `--muted` at 55%
opacity, drawn from `BRANDS`, which starts empty; while it's empty the whole band is hidden, never
an empty heading. Only logos Joshua supplies, of companies he worked for or with and has
permission to show (as for the Experience logos, §12). Logo
files must be one-color SVGs or PNGs with a transparent background, since each is painted in
`--muted` through a mask. Logos go to full opacity on hover, an exception to §11: these are
evidence a visitor may want to look at closely. Never merged with the tools marquee: that band
says "I use these", this one says "I worked with these".

**Services.** Four offers as plain columns separated by hairline rules: heading, then text. No
card surface, border, or radius, and no pricing. One column below 768px with rules between, two
from 768px (a two-by-two block, rules between the columns and between the rows), and four from
1180px. Not four at 1024px: each column would be too narrow to read comfortably.

**Stack.** Tools in four groups, in this order: Build, Automation & AI, Ship & infrastructure,
Design & tools. Each group is a `.label` above a grid of tool tiles (`.tool-tile`): the tool's
icon beside its name, one tile shape at every width, never a mix of square and wide tiles. Two
columns below 768px, four at 768px, five at 1024px, six from 1180px. Icons are 24px and one color,
`--text`, never brand colors: a grid of brand colors is noise, one color reads as a system. Tiles
aren't interactive, so they have no link, no focus, and no hover. Icons come from Simple Icons
(Slack and VS Code from Devicon), downloaded once and inlined as a sprite at the bottom of the page, never
loaded from a CDN. A tool with no official icon gets the same neutral placeholder glyph, not a
text-only tile; never draw an approximation of a company's logo.

**Certifications.** Twelve certificates: eleven from Anthropic, one from Google. Twelve uniform
cards in a row is monotonous, so group them under two subheads. Google comes first as a wide
feature card listing its seven courses, since it's the longer program; the Anthropic
certificates follow in a grid (one column, two from 768px, three from 1024px). One stat above
them: the count, captioned "certificates earned", in `--signal`. Titles are exactly as printed
on each certificate, and a date appears only when it's printed. Card images are 4:3 with the
whole certificate visible (letterboxed, never cropped). Clicking a card opens the full
certificate in a lightbox. A certificate with a verification link shows a small "Verify" link
(`.verify-link`) below the issuer, on the card and in the lightbox; it opens the issuer's page in
a new tab and never opens the lightbox. With no link, nothing shows: no dead or disabled link.
To keep the page short, the section shows the Google card and only as many Anthropic certificates
as fill complete rows, never a part-filled one: three in one column, six in two columns (three
rows), and six in three columns (two rows). The count follows the column count when the window is
resized. A button (`.btn--secondary`) reveals the rest in one step, with no animation beyond the
height change. It reads "Show all certificates", or "Show 1 more" when a single certificate is
left: a button promising "all" that adds one card overstates itself.

**Contact.** Plain text on the page background with a hairline rule above, like Services; not a
card. Heading and intro on the left; on the right, the availability line, the response time, the
location on two lines, an "Email me" button, and the channel list (email, LinkedIn, GitHub,
YouTube). No field labels, no numbers.

**Footer.** The name on the left with the year beneath in `--muted`; "Bacolod City,
Philippines" on the right with the links beneath. No middle dots.

---

## 7. Components

Build these once and reuse. Do not write bespoke markup per section.

- `.label` — section label with the monitor icon (`__icon`, `--icon-label`)
- `.section-head` — label + heading + optional deck
- `.btn` — variants `--primary`, `--secondary`, `--ghost`. The secondary button must carry its
  meaning in its label and text color, never in its border alone (`--line` is only 1.22–1.36:1
  against the background, which is right for a divider).
- `.card` — surface, border, radius. Variants: `--interactive` (the whole card opens
  something), `--feature` (wide, image beside text); `__media--contain` for documents that must
  never be cropped
- `.tag` — category tag
- `.verify-link` — small text link in the `.label` type and `--accent-text`, with a 24px tap
  target so it stays usable on top of a clickable card
- `.chip` — tech chip with optional icon. `--lg` when the chips are the content (the About
  capability chips)
- `.tool-tile` — a tool's 24px icon beside its name, on `--surface` with a `--line` border and
  `--r-sm`. An enlarged chip, not a card; never interactive. `.tool-grid` lays them out
- `.stat` — number + caption, with count-up hook. `__value--signal` for the certification count;
  `--compact` for the hero strip. `.stat-strip` lays several out in a row
- `.timeline-item` — row for Experience; its company and dates line can start with a `__logo`
  (fit to its kind's max width and height, `--wordmark` for lettering; grayscale until hovered) or
  a `__glyph` from the icon sprite
- `.pull-quote` — one sentence set apart: card-title size in `--text`, hairline rule above
- `.testimonial` — someone's words about the work in plain text: the quote, then "— source,
  detail", the source optionally linked. `--quiet` is smaller and all `--muted`, for a review
  under other text
- `.marquee` — a continuously scrolling row of one-color logos with a pause/play button; a
  static wrapped row under reduced motion
- `.activity` — the GitHub graph: a centered group (`__group`) of a `.label` with the GitHub mark
  (`__mark`), a fixed-size graph box (`__graph`) in a sideways-scrolling box (`__scroll`), and a
  profile link (`__link`); the whole block hides if the image fails to load
- `.brand-grid` — a static, centered row of one-color brand logos; hidden when there are none
- `.lightbox` — one image full size in a native `<dialog>`; Escape closes, focus returns to
  whatever opened it
- `.filters` / `.filter` — a group of toggle buttons; the selected one is an `--accent` fill
- `.card__phone` — a phone screenshot overlapping the corner of a card's screenshot
- `.work-list` / `.work-row` — the desktop Selected work list: one row per project, the name's
  link stretched over the row, an empty middle column (`__slot`) for the preview
- `.work-preview` — one fixed-position screenshot preview for the list; never in the layout,
  hidden from screen readers
- `.case-study` — a client project's three labeled lines (Problem, What I built, Result) as a
  description list, on the card and the list row
- `.personal-work` — the Personal projects block below Selected work: a `.label`, then each
  project's name link and short description, sized and spaced like the client projects above
  it, with no border and no preview
- `.contact-details` — availability, response time, location, and channel lines
- `.split` — text beside a side column from 1024px, stacked below

Repeated content (tools, marquee logos, brands, certificates, projects, experience, and the hero
stats) lives in data arrays at the top of the page script, each drawn by one template function.
Projects have one per layout (list row, preview image, card), all from the same array.

---

## 8. Motion

**One orchestrated moment, then nothing until the user acts**, with one recorded exception below.

- **Page load:** the hero animates in once — headline, then subhead, then buttons, then the
  stat strip, staggered by about 80ms. This is the site's one non-interactive moment.
- **Stat count-up:** runs once when the strip first enters the viewport.
- **Everything else is user-triggered:** card hover, nav state, filter changes, focus rings.
  Keep these at 180–250ms with a standard ease.
- **The Selected work preview** (§6) is user-triggered too: it fades in and out over 180ms
  (`--dur-fast`) and, while the visitor points, follows the cursor with a slight lag, then stops
  when the cursor stops. Keyboard focus holds it still.
- **The one exception: the tools marquee** (§6) scrolls on its own, one loop in about 40s. It is
  quiet, never shows the same logo twice on screen, has a visible pause button, and becomes a
  static row under reduced motion. No other element may move without the user acting.

**Do not add fade-and-slide-up reveals to every section on scroll.** I recommended this
earlier and I was wrong: scroll-triggered entrances on every section are the most recognizable
tell of a generated page, and on a page this long they make reading feel like it's fighting
back. One deliberate moment reads as designed; twelve read as a template.

`prefers-reduced-motion: reduce` disables the hero sequence, the count-up, the tools marquee,
and the Selected work preview's fade and cursor-follow (it appears at once, beside the row). Not
optional.

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
- Screenshots and photos in WebP; certificates and logos stay in their original format. Where
  a large original is only needed on demand (certificates in the lightbox), cards use a
  ~600px WebP thumbnail instead (`certifications/thumbs/`). All images sized to display
  dimensions, `loading="lazy"` below the fold
- Contrast: 4.5:1 body text, 3:1 large text, in **both** themes
- No layout shift on load — dimensions on every image

---

## 11. Things to avoid

Specific to this project, learned the hard way:

- Any type above 2.375rem outside the hero
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
- Cards for plain text blocks. Cards are for content with a thumbnail or an image.
  What separates a card from a chip is radius and shadow, not whether the content is an image.
  Cards use the card radius, `--r-md`. Small repeated items like tool tiles use `--r-sm` and never
  take a shadow: they're enlarged chips, not cards, and the card rules don't apply to them.
- Hover effects on anything that can't be clicked. A hover state promises an action. One
  recorded exception: brand logos (§6 Brands) go to full opacity on hover, and the Experience
  logos (§6 Experience) go from grayscale to full color, because they're evidence a visitor may
  want to look at closely. The tools marquee's logos and the Stack tiles
  get no hover: they list tools, and there's nothing more to see by pointing at them.

---

## 12. Open decisions

Tracked here so they don't get lost:

- [ ] Animation format and content
- [x] Whether Services shows pricing — no pricing shown
- [ ] Custom domain vs `.vercel.app`
- [ ] Case study pages for Rusty Mule and Rubens Removal
- [ ] Testimonials — one received (Mann Cayona, shown under his project); others still requested
- [x] Exact LSF job title and start date for the Experience entry — Claude Operator, July 2026
  (naming Lion Sales Funnels publicly still pending the contract check)
- [ ] Permission to show the Experience logos (Lion Sales Funnels, Roblox, VA House PH, American
  Express, Capital One) — added at Joshua's request in September 2026, before deploy
