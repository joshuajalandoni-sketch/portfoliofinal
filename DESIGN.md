# Portfolio design concept: jjoshua.vercel.app

This file is the design spec for my portfolio. Follow it when building or changing anything on the site.

**How to use with Claude Code:** "Read DESIGN.md and redesign the site to follow it. Keep my existing content and projects. Show me your plan before editing."

---

## The idea

Clean and editorial. A quiet, confident page where my photo builds trust and my real client websites prove the work.

**Signature element: the work stack.** In the hero, my photo sits in front of two or three real client-site screenshots, tucked behind it and slightly rotated, like a small pile of finished work. This is the one memorable thing on the page. Everything else stays calm and disciplined.

---

## Design tokens

### Color

| Name | Hex | Use |
|---|---|---|
| Paper | `#FAFAF7` | Page background |
| Ink | `#1A1D24` | Headings, body text, dark contact block |
| Graphite | `#5E6472` | Secondary text, client names |
| Hairline | `#E4E4DE` | Borders and dividers |
| Signal | `#2F5BFF` | The only accent: links, focus rings, primary button hover |
| Available | `#1F9D55` | "Available for work" dot only |

```css
:root {
  --paper: #FAFAF7;
  --ink: #1A1D24;
  --graphite: #5E6472;
  --hairline: #E4E4DE;
  --signal: #2F5BFF;
  --available: #1F9D55;
}
```

Rule: one accent color. Never add a second one.

### Typography

- **Typeface:** Schibsted Grotesk (Google Fonts) for everything. Weights 400, 500, and 700. One family keeps it clean.
- **Scale:**
  - Hero headline: `clamp(40px, 6vw, 64px)`, weight 700, line-height 1.05, letter-spacing -0.025em
  - Section headings (h2): 32px, weight 700, letter-spacing -0.015em
  - Project names (h3): 20px, weight 500
  - Body: 17px, weight 400, line-height 1.6
  - Small text: 14px
- Body text max width: 62ch.
- Sentence case everywhere. No all-caps labels.

### Layout

- Max content width 1120px, centered, 24px side padding (20px on mobile)
- Section spacing: 128px desktop, 80px mobile
- Everything left-aligned
- Corner radius: 16px for images and the contact block, 10px for buttons, fully rounded for the status pill
- No drop shadows except a very soft one under the stacked screenshots in the hero
- No gradients

### Motion

- **One page-load moment only:** headline appears, then my photo, then the screenshots slide out from behind it into their stacked positions. About 600ms total, ease-out.
- After that, motion only responds to the visitor: project screenshots scale to 1.03 on hover; buttons change color on hover.
- No fade-in on every section while scrolling.
- `prefers-reduced-motion`: everything appears in place with no movement.

---

## Page structure

```
┌──────────────────────────────────────────────────────┐
│ Joshua Jalandoni          Work  About  Contact  ● Available │
├──────────────────────────────────────────────────────┤
│                                                      │
│  I design websites that        ┌──┐┌───────┐         │
│  make small businesses         │▒▒││ PHOTO │         │  ← hero + work stack
│  look legit.                   │▒▒││  4:5  │         │
│                                └──┘└───────┘         │
│  Short subline                                       │
│  [See my work]  [Email me]                           │
│                                                      │
├──────────────────────────────────────────────────────┤
│ Rusty Mule Pizza  Rubens Removal  Pinoy Eats  ...    │  ← client strip
├──────────────────────────────────────────────────────┤
│ Selected work                                        │
│ ┌────────────┐  ┌────────────┐                       │
│ │ screenshot │  │ screenshot │                       │  ← 2-column grid
│ └────────────┘  └────────────┘                       │
│ Name / one line  Name / one line                     │
├──────────────────────────────────────────────────────┤
│ What I do:  Design  |  Build and launch  |  (third)  │
├──────────────────────────────────────────────────────┤
│ About: short paragraph + tools                       │
├──────────────────────────────────────────────────────┤
│ ████ Need a website? Let's build it.  [Email me] ████ │  ← dark ink block
├──────────────────────────────────────────────────────┤
│ Footer                                               │
└──────────────────────────────────────────────────────┘
```

### 1. Nav
- Left: "Joshua Jalandoni" (weight 500)
- Right: Work, About, Contact, plus a small pill with a green dot: "Available for work"
- Sticky on scroll with a Paper background and a Hairline bottom border
- Mobile: name on the left, simple menu button on the right

### 2. Hero
- Two columns on desktop (text about 55%, work stack about 45%). On mobile, the photo comes first, then the text.
- Headline: **"I design websites that make small businesses look legit."**
- Subline: "Fast, clean sites for restaurants, service businesses, and creators. Designed, built, and launched."
- Buttons: "See my work" (solid Ink, scrolls to the work section) and "Email me" (outline, opens mailto)
- Work stack: my photo `/public/me.jpg` in a 4:5 frame with 16px radius, in front. Two screenshots from `/public/work/` sit behind it, offset and rotated about -4° and 3°, with the soft shadow.

### 3. Client strip
- My client names in Graphite, evenly spaced, with a Hairline border above and below
- Rusty Mule Pizza, Rubens Removal LLC, Pinoy Eats, Mann Cayona, Berserk
- If I add client logos later, show them in grayscale at the same height

### 4. Selected work
- Heading: "Selected work"
- 2-column grid on desktop, 1 column on mobile, 32px gap
- Each project: screenshot in a 16:10 frame (16px radius, Hairline border), project name, one line about what the business needed, and a "Visit site" link
- Put the strongest project first

| Project | One line (edit these) | Image |
|---|---|---|
| Rusty Mule Pizza | Restaurant site with menu and ordering | `/public/work/rusty-mule.webp` |
| Rubens Removal LLC | Service business site built to get quote requests | `/public/work/rubens-removal.webp` |
| Pinoy Eats | [what it needed] | `/public/work/pinoy-eats.webp` |
| Mann Cayona | [what it needed] | `/public/work/mann-cayona.webp` |
| Berserk | [what it needed] | `/public/work/berserk.webp` |

### 5. Services
- Heading: "What I do"
- Three columns, each with a short title and one sentence. No icons.
  - **Website design:** a layout that fits your business and your customers
  - **Build and launch:** fast, mobile-friendly sites, deployed and live
  - **[Third service]:** e.g. automation, updates and maintenance, or landing pages

### 6. About
- Optional second photo (candid, working at a desk)
- 2–3 sentences about who I am and how I work
- Tools I use: Figma, Claude Code, GitHub, Vercel (plain text list)

### 7. Contact
- Full-width Ink block, 16px radius, Paper-colored text
- Headline: "Need a website? Let's build it."
- One button: "Email me" (mailto link), plus social links

### 8. Footer
- Name, year, and social links in small Graphite text

---

## Photo guide

- Face a window in daylight; no overhead lights or flash
- Plain wall behind me, or remove the background and place me on Paper or a light gray
- Frame from the chest up and crop to 4:5
- Relaxed smile or calm neutral face
- Plain dark or neutral top, no busy patterns
- Export as WebP, about 1200px tall

---

## Technical requirements

- **Remove the "Unpacking..." loader completely.** Content must be real HTML on first load, so Google and link previews on Messenger and LinkedIn can see it.
- Proper `<title>`: "Joshua Jalandoni: Web Designer and Developer"
- Meta description, favicon, and an Open Graph image (1200×630) with my photo and name
- Images in WebP with explicit width and height, and lazy-loaded below the hero
- Fully responsive: 1 column under 768px
- Accessible: alt text on every image, visible focus rings in Signal blue, and text contrast of at least 4.5:1
- Lighthouse score 90+ on performance and accessibility

---

## Don'ts

- No second accent color
- No gradients, glow, or heavy shadows
- No all-caps labels or little tags above every heading
- No fade-in animation on every section
- No icon clutter
- No loading screen
- Don't break the rule of one memorable thing: the work stack is the star

---

## Before shipping

- [ ] My photo is in `/public/me.jpg`
- [ ] Screenshots are in `/public/work/`
- [ ] Project one-liners are filled in
- [ ] Email and social links work
- [ ] Looks good on my phone
- [ ] Link preview shows my photo and name when shared
