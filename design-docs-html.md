# Premium HTML Documentation Design System
> Hand this file to any AI agent along with your project content.
> The agent will produce a single-file, production-quality HTML documentation page.

---

## ★ HOW TO USE THIS DOCUMENT

Give the agent this file plus the following instructions:

```
Read design.md fully before writing any code.

My project: [YOUR PROJECT NAME]
Palette choice: [PALETTE NAME from Section 2, or "Custom" with your hex values]
Font choice: [FONT PAIR NAME from Section 3, or "Custom" with your font names]
Sections needed: [e.g. Overview, Architecture, API Reference, Setup, Changelog]

Follow every rule in design.md exactly.
Produce a single self-contained HTML file with all CSS and JS inline.
Do not use any external CSS frameworks (Tailwind, Bootstrap, etc.).
Only external resources allowed: Google Fonts CDN + Mermaid CDN (if diagrams needed).
```

---

## 1. DESIGN PHILOSOPHY

### Core Principles

**Token-first architecture.** Every colour, spacing unit, and font is a CSS custom property. Never hardcode a hex value inside a CSS rule — always use `var(--token-name)`. This is what makes dark mode work automatically and makes the whole file themeable.

**Three font roles.** Every premium doc uses exactly three font roles: a characterful *display* face for headings, a highly-readable *body* face for prose, and a crisp *mono* face for code, labels, and data. These three roles create typographic hierarchy without effort.

**Dark mode is automatic, not bolted on.** Use `@media (prefers-color-scheme: dark)` to redefine tokens — not to write duplicate rules. The entire page flips because every element only references tokens.

**Layered backgrounds.** A flat colour background is Simple tier. Premium backgrounds layer: base colour + radial gradient glow + subtle texture (grid lines, dot grid, or noise). All via CSS, no images.

**Glassmorphism navigation.** The sticky nav uses `backdrop-filter: blur()` + a semi-transparent background. This is the most immediately visible "premium" signal.

**Staggered entrance animations.** Elements animate in with `fadeUp` or `fadeScale` on load, staggered with `animation-delay`. Always include a `prefers-reduced-motion` guard that disables animations for users who need it.

**Signature element.** Every page has one element that would be remembered — an oversized italic serif headline, a grid-texture background, interactive diagrams, or a unique hero layout. Choose one and commit to it.

### What NOT to do

- Do not use Tailwind, Bootstrap, or any utility-class framework
- Do not use pure `#000000` black or `#ffffff` white anywhere in the palette
- Do not hardcode colours — only `var(--token)` in CSS rules
- Do not use more than 3 Google Font families
- Do not add animations without a `prefers-reduced-motion` guard
- Do not forget semantic HTML (`<main>`, `<section>`, `<nav>`, `<header>`, `<footer>`)
- Do not use `px` for font sizes in the hero — use `clamp()` for fluid scaling

---

## 2. COLOUR SYSTEM

### How the Token System Works

Define all colours once in `:root` (light theme values). Override the same variable names inside `@media (prefers-color-scheme: dark)`. Every CSS rule uses only `var(--token)` — never a raw hex.

**Required token names (agent must use these exact names):**

| Token | Purpose |
|---|---|
| `--bg` | Page background |
| `--bg-tint` | Slightly darker bg — for section separators, tinted rows |
| `--surface` | Card / panel background |
| `--surface-up` | Elevated surface — modals, dropdowns |
| `--border` | Default border colour (low opacity) |
| `--border-hi` | Highlighted border (hover, focus) |
| `--text` | Body text |
| `--text-bright` | Headings, strong emphasis |
| `--text-dim` | Secondary text, captions, labels |
| `--accent` | Primary brand accent — links, highlights, icons |
| `--accent-dim` | 10–15% opacity version of accent — badge backgrounds, hover fills |
| `--accent-bright` | Brighter/lighter version for dark mode contrast |
| `--success` | Positive / success states (usually green/sage) |
| `--success-dim` | 10–14% opacity version |
| `--warning` | Warning / caution states (usually amber) |
| `--warning-dim` | 10–14% opacity version |
| `--danger` | Error / danger states (usually rose/red) |
| `--danger-dim` | 10–14% opacity version |
| `--code-bg` | Code block background (usually near-black even in light mode) |
| `--code-text` | Code block text |
| `--code-accent` | Syntax highlight: keywords |
| `--code-string` | Syntax highlight: strings/values |
| `--code-comment` | Syntax highlight: comments |
| `--font-display` | Display font stack |
| `--font-body` | Body font stack |
| `--font-mono` | Monospace font stack |

---

### PALETTE A — Editorial Gold
*Mood: luxury reference book, blueprint, editorial magazine*
*Best for: technical specs, design systems, architecture docs*

```css
/* ── LIGHT ── */
:root {
  --bg:             #f7f3eb;
  --bg-tint:        #efe9dc;
  --surface:        #fdfbf6;
  --surface-up:     #ffffff;
  --border:         rgba(30, 58, 95, 0.12);
  --border-hi:      rgba(30, 58, 95, 0.25);
  --text:           #1c2a3a;
  --text-bright:    #0d1a2c;
  --text-dim:       #6a7689;
  --accent:         #b8923a;
  --accent-dim:     rgba(184, 146, 58, 0.12);
  --accent-bright:  #9c7a26;
  --success:        #5b7a3a;
  --success-dim:    rgba(91, 122, 58, 0.12);
  --warning:        #c47a1a;
  --warning-dim:    rgba(196, 122, 26, 0.12);
  --danger:         #a8324a;
  --danger-dim:     rgba(168, 50, 74, 0.10);
  --code-bg:        #1a2636;
  --code-text:      #c8daf0;
  --code-accent:    #7ec8e3;
  --code-string:    #a8d8a8;
  --code-comment:   #607080;
}

/* ── DARK ── */
@media (prefers-color-scheme: dark) {
  :root {
    --bg:             #0d1a2c;
    --bg-tint:        #0a1626;
    --surface:        #122238;
    --surface-up:     #16294a;
    --border:         rgba(228, 207, 156, 0.10);
    --border-hi:      rgba(228, 207, 156, 0.22);
    --text:           #e4cf9c;
    --text-bright:    #f4e3b8;
    --text-dim:       #93a0b3;
    --accent:         #d4a73a;
    --accent-dim:     rgba(212, 167, 58, 0.16);
    --accent-bright:  #e4cf9c;
    --success:        #9fc35a;
    --success-dim:    rgba(159, 195, 90, 0.14);
    --warning:        #e8a958;
    --warning-dim:    rgba(232, 169, 88, 0.14);
    --danger:         #d96384;
    --danger-dim:     rgba(217, 99, 132, 0.14);
    --code-bg:        #060f1a;
    --code-text:      #c8daf0;
    --code-accent:    #7ec8e3;
    --code-string:    #a8d8a8;
    --code-comment:   #4a5e70;
  }
}
```

---

### PALETTE B — Blueprint Indigo
*Mood: modern SaaS, technical product, engineering team*
*Best for: API references, developer docs, open-source projects*

```css
/* ── LIGHT ── */
:root {
  --bg:             #f0f4ff;
  --bg-tint:        #e4ebff;
  --surface:        #fafbff;
  --surface-up:     #ffffff;
  --border:         rgba(15, 27, 75, 0.11);
  --border-hi:      rgba(15, 27, 75, 0.24);
  --text:           #0f1b35;
  --text-bright:    #060e22;
  --text-dim:       #5a6882;
  --accent:         #3b5bdb;
  --accent-dim:     rgba(59, 91, 219, 0.10);
  --accent-bright:  #2a44b8;
  --success:        #0ca678;
  --success-dim:    rgba(12, 166, 120, 0.12);
  --warning:        #e07b2a;
  --warning-dim:    rgba(224, 123, 42, 0.12);
  --danger:         #e03131;
  --danger-dim:     rgba(224, 49, 49, 0.10);
  --code-bg:        #0f1b35;
  --code-text:      #c8d8f0;
  --code-accent:    #74b0ff;
  --code-string:    #8fd4a8;
  --code-comment:   #4a6080;
}

/* ── DARK ── */
@media (prefers-color-scheme: dark) {
  :root {
    --bg:             #0b1220;
    --bg-tint:        #080e1a;
    --surface:        #0f1830;
    --surface-up:     #152040;
    --border:         rgba(116, 176, 255, 0.10);
    --border-hi:      rgba(116, 176, 255, 0.22);
    --text:           #b8cef0;
    --text-bright:    #daeaff;
    --text-dim:       #6080a8;
    --accent:         #74b0ff;
    --accent-dim:     rgba(116, 176, 255, 0.14);
    --accent-bright:  #a0ccff;
    --success:        #4ecda0;
    --success-dim:    rgba(78, 205, 160, 0.14);
    --warning:        #ffaa40;
    --warning-dim:    rgba(255, 170, 64, 0.14);
    --danger:         #ff6b6b;
    --danger-dim:     rgba(255, 107, 107, 0.14);
    --code-bg:        #040810;
    --code-text:      #b8cef0;
    --code-accent:    #74b0ff;
    --code-string:    #8fd4a8;
    --code-comment:   #3a5068;
  }
}
```

---

### PALETTE C — Midnight Copper
*Mood: premium dark-first, forge, metalwork, high-end technical*
*Best for: dark-preferred audiences, CLI tools, system docs*

```css
/* ── LIGHT ── */
:root {
  --bg:             #f6f2ea;
  --bg-tint:        #ede8dc;
  --surface:        #fdfbf7;
  --surface-up:     #ffffff;
  --border:         rgba(30, 40, 60, 0.11);
  --border-hi:      rgba(30, 40, 60, 0.24);
  --text:           #1e2c3a;
  --text-bright:    #0d1a28;
  --text-dim:       #68788c;
  --accent:         #b5631a;
  --accent-dim:     rgba(181, 99, 26, 0.12);
  --accent-bright:  #9a4e0d;
  --success:        #4a7c59;
  --success-dim:    rgba(74, 124, 89, 0.12);
  --warning:        #b87a10;
  --warning-dim:    rgba(184, 122, 16, 0.12);
  --danger:         #a03040;
  --danger-dim:     rgba(160, 48, 64, 0.10);
  --code-bg:        #1a2636;
  --code-text:      #c8daf0;
  --code-accent:    #e08040;
  --code-string:    #9fcf88;
  --code-comment:   #5a7080;
}

/* ── DARK ── */
@media (prefers-color-scheme: dark) {
  :root {
    --bg:             #0e1b2c;
    --bg-tint:        #0a1522;
    --surface:        #132030;
    --surface-up:     #1a2940;
    --border:         rgba(224, 140, 64, 0.10);
    --border-hi:      rgba(224, 140, 64, 0.24);
    --text:           #d8c8a0;
    --text-bright:    #f0e4c0;
    --text-dim:       #7a90a8;
    --accent:         #e08040;
    --accent-dim:     rgba(224, 128, 64, 0.15);
    --accent-bright:  #f0a060;
    --success:        #7ec87a;
    --success-dim:    rgba(126, 200, 122, 0.14);
    --warning:        #e8b050;
    --warning-dim:    rgba(232, 176, 80, 0.14);
    --danger:         #e07090;
    --danger-dim:     rgba(224, 112, 144, 0.14);
    --code-bg:        #060f1a;
    --code-text:      #c8d4e0;
    --code-accent:    #e08040;
    --code-string:    #9fcf88;
    --code-comment:   #4a6070;
  }
}
```

---

### PALETTE D — Forest Sage
*Mood: calm, natural, thoughtful, sustainable tech*
*Best for: data docs, research papers, environmental/science projects*

```css
/* ── LIGHT ── */
:root {
  --bg:             #f2f5f0;
  --bg-tint:        #e8ede4;
  --surface:        #fafcf8;
  --surface-up:     #ffffff;
  --border:         rgba(20, 50, 30, 0.11);
  --border-hi:      rgba(20, 50, 30, 0.24);
  --text:           #1a2e22;
  --text-bright:    #0c1e14;
  --text-dim:       #5e7868;
  --accent:         #2d7a4a;
  --accent-dim:     rgba(45, 122, 74, 0.11);
  --accent-bright:  #1e5c36;
  --success:        #3a9e5c;
  --success-dim:    rgba(58, 158, 92, 0.12);
  --warning:        #c08020;
  --warning-dim:    rgba(192, 128, 32, 0.12);
  --danger:         #b83030;
  --danger-dim:     rgba(184, 48, 48, 0.10);
  --code-bg:        #1a2620;
  --code-text:      #c0d8c4;
  --code-accent:    #68d888;
  --code-string:    #d8c880;
  --code-comment:   #4a6850;
}

/* ── DARK ── */
@media (prefers-color-scheme: dark) {
  :root {
    --bg:             #0e1a12;
    --bg-tint:        #0a140d;
    --surface:        #121e14;
    --surface-up:     #182618;
    --border:         rgba(120, 200, 140, 0.10);
    --border-hi:      rgba(120, 200, 140, 0.22);
    --text:           #b8d8b8;
    --text-bright:    #d8f0d8;
    --text-dim:       #6a8e6a;
    --accent:         #5ec87a;
    --accent-dim:     rgba(94, 200, 122, 0.14);
    --accent-bright:  #90e8a0;
    --success:        #6ed490;
    --success-dim:    rgba(110, 212, 144, 0.14);
    --warning:        #e8c050;
    --warning-dim:    rgba(232, 192, 80, 0.14);
    --danger:         #e06060;
    --danger-dim:     rgba(224, 96, 96, 0.14);
    --code-bg:        #060e08;
    --code-text:      #b8d8b8;
    --code-accent:    #68d888;
    --code-string:    #d8c880;
    --code-comment:   #3a5840;
  }
}
```

---

### PALETTE E — Obsidian Violet
*Mood: bold, creative, modern studio, design tool*
*Best for: creative projects, design system docs, portfolio*

```css
/* ── LIGHT ── */
:root {
  --bg:             #f4f0fb;
  --bg-tint:        #ebe4f6;
  --surface:        #fbf9fe;
  --surface-up:     #ffffff;
  --border:         rgba(50, 20, 90, 0.11);
  --border-hi:      rgba(50, 20, 90, 0.24);
  --text:           #22143a;
  --text-bright:    #120a22;
  --text-dim:       #7060a0;
  --accent:         #7c3aed;
  --accent-dim:     rgba(124, 58, 237, 0.10);
  --accent-bright:  #6020d0;
  --success:        #0f9e6e;
  --success-dim:    rgba(15, 158, 110, 0.12);
  --warning:        #d4820e;
  --warning-dim:    rgba(212, 130, 14, 0.12);
  --danger:         #c0283c;
  --danger-dim:     rgba(192, 40, 60, 0.10);
  --code-bg:        #1a1028;
  --code-text:      #d0c0f0;
  --code-accent:    #c084fc;
  --code-string:    #86efac;
  --code-comment:   #604880;
}

/* ── DARK ── */
@media (prefers-color-scheme: dark) {
  :root {
    --bg:             #0e0818;
    --bg-tint:        #0a0614;
    --surface:        #140c22;
    --surface-up:     #1c1230;
    --border:         rgba(196, 132, 252, 0.10);
    --border-hi:      rgba(196, 132, 252, 0.22);
    --text:           #d0b8f0;
    --text-bright:    #f0e0ff;
    --text-dim:       #806090;
    --accent:         #c084fc;
    --accent-dim:     rgba(196, 132, 252, 0.15);
    --accent-bright:  #ddb0ff;
    --success:        #4ade80;
    --success-dim:    rgba(74, 222, 128, 0.14);
    --warning:        #facc15;
    --warning-dim:    rgba(250, 204, 21, 0.14);
    --danger:         #f87171;
    --danger-dim:     rgba(248, 113, 113, 0.14);
    --code-bg:        #06020e;
    --code-text:      #d0c0f0;
    --code-accent:    #c084fc;
    --code-string:    #86efac;
    --code-comment:   #483660;
  }
}
```

---

### CUSTOM PALETTE TEMPLATE
*Use this when the user provides their own colours*

```css
/* Fill in your brand hex values below, then derive the dim variants
   by adding opacity. Rule: dim = colour at 10-15% opacity */

:root {
  /* ── Backgrounds ── */
  --bg:             #______;   /* warm, not pure white — e.g. #f7f3eb */
  --bg-tint:        #______;   /* 5-8% darker than --bg */
  --surface:        #______;   /* close to white — card/panel bg */
  --surface-up:     #ffffff;   /* purest elevated surface */

  /* ── Borders ── */
  --border:         rgba(R, G, B, 0.11);  /* use --text-bright's RGB */
  --border-hi:      rgba(R, G, B, 0.24);

  /* ── Text ── */
  --text:           #______;   /* dark but not #000 — e.g. #1c2a3a */
  --text-bright:    #______;   /* 10-15% darker than --text */
  --text-dim:       #______;   /* 50-60% opacity equivalent of --text */

  /* ── Accent (your brand colour) ── */
  --accent:         #______;   /* your brand colour */
  --accent-dim:     rgba(R, G, B, 0.12);
  --accent-bright:  #______;   /* 15% darker shade */

  /* ── Status Colours ── */
  --success:        #______;   /* green / teal */
  --success-dim:    rgba(R, G, B, 0.12);
  --warning:        #______;   /* amber / orange */
  --warning-dim:    rgba(R, G, B, 0.12);
  --danger:         #______;   /* red / rose */
  --danger-dim:     rgba(R, G, B, 0.10);

  /* ── Code Block ── */
  --code-bg:        #______;   /* near-black, e.g. #1a2636 */
  --code-text:      #______;   /* light blue-grey, e.g. #c8daf0 */
  --code-accent:    #______;   /* keyword colour */
  --code-string:    #______;   /* string colour */
  --code-comment:   #______;   /* comment colour (dim) */
}

/* Dark mode: flip bg↔text, brighten accent slightly, add warmth to text */
@media (prefers-color-scheme: dark) {
  :root {
    --bg:             #______;   /* deep — e.g. #0d1a2c */
    --bg-tint:        #______;   /* 5% darker than dark --bg */
    --surface:        #______;   /* card bg in dark — e.g. #122238 */
    --surface-up:     #______;   /* slightly lighter than --surface */
    --border:         rgba(R, G, B, 0.10);  /* use accent or bright-text RGB */
    --border-hi:      rgba(R, G, B, 0.22);
    --text:           #______;   /* warm, not cold white — e.g. #e4cf9c */
    --text-bright:    #______;   /* slightly brighter than --text */
    --text-dim:       #______;   /* muted version */
    --accent:         #______;   /* slightly brighter than light version */
    --accent-dim:     rgba(R, G, B, 0.15);
    --accent-bright:  #______;   /* lightest accent — for text on dark */
    --success:        #______;   /* brighter green */
    --success-dim:    rgba(R, G, B, 0.14);
    --warning:        #______;   /* brighter amber */
    --warning-dim:    rgba(R, G, B, 0.14);
    --danger:         #______;   /* brighter rose */
    --danger-dim:     rgba(R, G, B, 0.14);
  }
}
```

---

## 3. TYPOGRAPHY SYSTEM

### Font Roles (always 3)

| Role | CSS Token | Usage |
|---|---|---|
| Display | `--font-display` | Hero h1, section h2, card h3, pull-quotes. Set in italic for personality. |
| Body | `--font-body` | All body text, paragraphs, descriptions, UI copy |
| Mono | `--font-mono` | Code blocks, nav links, section eyebrows, data labels, badges |

---

### FONT PAIR A — Instrument × Inter Tight *(your spec.html pair)*
*Mood: refined, technical, editorial precision*

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@0;1&family=Inter+Tight:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
```
```css
:root {
  --font-display: 'Instrument Serif', 'Iowan Old Style', Georgia, serif;
  --font-body:    'Inter Tight', system-ui, sans-serif;
  --font-mono:    'JetBrains Mono', 'SF Mono', Consolas, monospace;
}
```
*Hero headline: weight 400, italic, letter-spacing -2px*
*Body: weight 400 regular, line-height 1.6*
*Labels: weight 600, uppercase, letter-spacing 2px*

---

### FONT PAIR B — Fraunces × DM Sans
*Mood: warm editorial, magazine, considered craftsmanship*

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,300;0,9..144,600;1,9..144,300;1,9..144,600&family=DM+Sans:wght@300;400;500;600&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
```
```css
:root {
  --font-display: 'Fraunces', 'Iowan Old Style', Georgia, serif;
  --font-body:    'DM Sans', system-ui, sans-serif;
  --font-mono:    'JetBrains Mono', 'SF Mono', Consolas, monospace;
}
```
*Hero headline: weight 300, italic (Fraunces optical size renders beautifully)*
*Body: weight 400, line-height 1.65*
*Labels: weight 600, uppercase, letter-spacing 2px*

---

### FONT PAIR C — DM Serif Display × Plus Jakarta Sans
*Mood: modern product, SaaS, confident and readable*

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=Plus+Jakarta+Sans:wght@300;400;500;600;700&family=Fira+Code:wght@400;500&display=swap" rel="stylesheet">
```
```css
:root {
  --font-display: 'DM Serif Display', Georgia, serif;
  --font-body:    'Plus Jakarta Sans', system-ui, sans-serif;
  --font-mono:    'Fira Code', 'SF Mono', Consolas, monospace;
}
```
*Hero headline: weight 400, letter-spacing -1.5px*
*Body: weight 400, line-height 1.65*
*Labels: weight 500, uppercase, letter-spacing 1.8px*

---

### FONT PAIR D — Space Grotesk × IBM Plex Mono *(Blueprint / Engineering)*
*Mood: blueprint, technical specs, no-nonsense engineering*

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=IBM+Plex+Mono:ital,wght@0,400;0,500;0,600;1,400&display=swap" rel="stylesheet">
```
```css
:root {
  --font-display: 'Space Grotesk', system-ui, sans-serif;
  --font-body:    'Space Grotesk', system-ui, sans-serif;
  --font-mono:    'IBM Plex Mono', 'SF Mono', Consolas, monospace;
}
```
*Hero headline: weight 700, letter-spacing -2px, text-transform uppercase optional*
*Body: weight 400, line-height 1.6*
*Labels: mono, weight 600, uppercase, letter-spacing 3px*

---

### FONT PAIR E — Playfair Display × Source Sans 3
*Mood: classic, academic, timeless documentation*

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400;1,700&family=Source+Sans+3:wght@300;400;600&family=Cascadia+Code:wght@400;500&display=swap" rel="stylesheet">
```
```css
:root {
  --font-display: 'Playfair Display', Georgia, serif;
  --font-body:    'Source Sans 3', system-ui, sans-serif;
  --font-mono:    'Cascadia Code', 'SF Mono', Consolas, monospace;
}
```
*Hero headline: weight 400 or 700, italic variant for em tags*
*Body: weight 400, line-height 1.7 (slightly more generous)*
*Labels: Source Sans 3, weight 600, uppercase, letter-spacing 1.5px*

---

### CUSTOM FONT TEMPLATE

```html
<!-- Replace with chosen fonts from fonts.google.com -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=DISPLAY_FONT&family=BODY_FONT&family=MONO_FONT&display=swap" rel="stylesheet">
```
```css
:root {
  --font-display: 'Display Font Name', Georgia, serif;    /* or sans-serif */
  --font-body:    'Body Font Name', system-ui, sans-serif;
  --font-mono:    'Mono Font Name', 'SF Mono', Consolas, monospace;
}
```

---

## 4. COMPLETE CSS FOUNDATION

*Paste this after the token definitions. Do not modify — all values reference tokens.*

```css
/* ══════════════════════════════════════
   RESET
══════════════════════════════════════ */
*, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
body { overflow-wrap: break-word; -webkit-font-smoothing: antialiased; }

/* ══════════════════════════════════════
   BASE
══════════════════════════════════════ */
body {
  background-color: var(--bg);
  color: var(--text);
  font-family: var(--font-body);
  font-size: 16px;
  line-height: 1.6;
  min-height: 100vh;
}

::selection {
  background: var(--accent-dim);
  color: var(--text-bright);
}

/* ══════════════════════════════════════
   BACKGROUND LAYER  (choose one style)
══════════════════════════════════════ */

/* Style 1: Radial glow + grid lines (Editorial × Blueprint) */
body {
  background-image:
    radial-gradient(ellipse at 55% -8%, var(--accent-dim) 0%, transparent 52%),
    radial-gradient(ellipse at 5% 85%, var(--success-dim) 0%, transparent 38%),
    repeating-linear-gradient(0deg,   transparent, transparent 47px, var(--border) 47px, var(--border) 48px),
    repeating-linear-gradient(90deg,  transparent, transparent 47px, var(--border) 47px, var(--border) 48px);
  background-attachment: fixed;
}

/* Style 2: Radial glow only (clean, subtle) */
/*
body {
  background-image:
    radial-gradient(ellipse at 60% -10%, var(--accent-dim) 0%, transparent 50%),
    radial-gradient(ellipse at 10% 90%, var(--success-dim) 0%, transparent 40%);
  background-attachment: fixed;
}
*/

/* Style 3: Dot grid */
/*
body {
  background-image:
    radial-gradient(circle, var(--border-hi) 1px, transparent 1px);
  background-size: 28px 28px;
}
*/

/* ══════════════════════════════════════
   ANIMATIONS
══════════════════════════════════════ */
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(16px); }
  to   { opacity: 1; transform: translateY(0); }
}
@keyframes fadeScale {
  from { opacity: 0; transform: scale(0.94); }
  to   { opacity: 1; transform: scale(1); }
}
@keyframes fadeIn {
  from { opacity: 0; }
  to   { opacity: 1; }
}

/* Stagger via inline style="--i:1" etc. on the element */
.anim       { animation: fadeUp   0.5s cubic-bezier(0.2, 0.7, 0.2, 1) both; animation-delay: calc(var(--i, 0) * 0.06s); }
.anim-scale { animation: fadeScale 0.4s ease-out both;                       animation-delay: calc(var(--i, 0) * 0.06s); }
.anim-fade  { animation: fadeIn    0.4s ease both;                           animation-delay: calc(var(--i, 0) * 0.06s); }

/* Accessibility: disable animations if user prefers */
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration:   0.01ms !important;
    animation-delay:      0ms   !important;
    transition-duration:  0.01ms !important;
  }
}

/* ══════════════════════════════════════
   LAYOUT
══════════════════════════════════════ */
.shell {
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 28px 100px;
}

/* ══════════════════════════════════════
   TYPOGRAPHY SCALE
══════════════════════════════════════ */
h1 {
  font-family: var(--font-display);
  font-size: clamp(46px, 5.8vw, 82px);
  font-weight: 400;
  line-height: 1.0;
  letter-spacing: -1.5px;
  color: var(--text-bright);
}
h1 em { font-style: italic; color: var(--accent); }

h2 {
  font-family: var(--font-display);
  font-size: clamp(28px, 3vw, 42px);
  font-weight: 400;
  line-height: 1.15;
  letter-spacing: -0.8px;
  color: var(--text-bright);
}
h2 em { font-style: italic; color: var(--accent); }

h3 {
  font-family: var(--font-display);
  font-size: clamp(18px, 2vw, 22px);
  font-weight: 600;
  color: var(--text-bright);
}

p  { font-size: 16px; line-height: 1.65; color: var(--text); }
li { font-size: 15px; line-height: 1.7; color: var(--text); }

a  { color: var(--accent); text-underline-offset: 3px; }
a:hover { color: var(--accent-bright); }

code {
  font-family: var(--font-mono);
  font-size: 0.88em;
  background: var(--bg-tint);
  color: var(--accent);
  padding: 2px 6px;
  border-radius: 4px;
}

pre code { background: none; color: inherit; padding: 0; }
```

---

## 5. COMPONENT LIBRARY

### 5.1 — Sticky Glassmorphism Navigation

```html
<nav class="nav" role="navigation" aria-label="Page sections">
  <div class="nav__inner">
    <span class="nav__brand">PROJECT NAME</span>
    <a href="#section-id-1">Section One</a>
    <a href="#section-id-2">Section Two</a>
    <a href="#section-id-3">Section Three</a>
    <!-- add more links as needed -->
  </div>
</nav>
```

```css
.nav {
  position: sticky;
  top: 0;
  z-index: 60;
  backdrop-filter: blur(14px);
  -webkit-backdrop-filter: blur(14px);
  background: color-mix(in srgb, var(--bg) 76%, transparent);
  border-bottom: 1px solid var(--border);
  padding: 13px 28px;
  margin: 0 -28px 0;   /* bleed to edge inside .shell */
}
.nav__inner {
  max-width: 1044px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  gap: 4px;
  overflow-x: auto;
  scrollbar-width: none;
}
.nav__inner::-webkit-scrollbar { display: none; }
.nav__brand {
  font-family: var(--font-mono);
  font-size: 10.5px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 2px;
  color: var(--accent);
  padding-right: 16px;
  margin-right: 8px;
  border-right: 1px solid var(--border);
  white-space: nowrap;
  flex-shrink: 0;
}
.nav a {
  font-family: var(--font-mono);
  font-size: 10.5px;
  color: var(--text-dim);
  text-decoration: none;
  padding: 6px 10px;
  border-radius: 5px;
  white-space: nowrap;
  transition: color 0.15s, background 0.15s;
}
.nav a:hover { color: var(--text); background: var(--accent-dim); }
```

---

### 5.2 — Hero Section

```html
<header class="hero" role="banner">
  <div class="hero__eyebrow anim" style="--i:0">Implementation Spec · v1.0</div>
  <h1 class="anim" style="--i:1">
    Your project<br><em>beautifully</em> documented
  </h1>
  <p class="hero__sub anim" style="--i:2">
    One sentence that says exactly what this document covers and who it is for.
  </p>
  <div class="hero__meta anim" style="--i:3">
    <span class="badge badge--accent">Status: Draft</span>
    <span class="badge badge--success">v1.0.0</span>
    <span class="badge badge--mono">Last updated: [DATE]</span>
  </div>
</header>
```

```css
.hero {
  padding: 52px 0 60px;
  border-bottom: 1px solid var(--border);
  margin-bottom: 64px;
}
.hero__eyebrow {
  font-family: var(--font-mono);
  font-size: 10.5px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 2.5px;
  color: var(--accent);
  display: inline-flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 20px;
}
.hero__eyebrow::before {
  content: '';
  width: 22px;
  height: 1px;
  background: var(--accent);
}
/* h1 styles already defined in Typography Scale */
.hero__sub {
  font-family: var(--font-display);
  font-style: italic;
  font-size: clamp(18px, 2vw, 24px);
  color: var(--text-dim);
  line-height: 1.4;
  max-width: 640px;
  margin: 20px 0 28px;
}
.hero__meta {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}
```

---

### 5.3 — Badges

```html
<!-- Usage: add one class from each group below -->
<span class="badge badge--accent">Primary Accent</span>
<span class="badge badge--success">Success / Done</span>
<span class="badge badge--warning">Warning / WIP</span>
<span class="badge badge--danger">Danger / Deprecated</span>
<span class="badge badge--mono">Plain Label</span>
```

```css
.badge {
  display: inline-flex;
  align-items: center;
  gap: 5px;
  font-family: var(--font-mono);
  font-size: 10.5px;
  font-weight: 500;
  padding: 4px 10px;
  border-radius: 5px;
  letter-spacing: 0.5px;
}
.badge--accent  { color: var(--accent);  background: var(--accent-dim);  border: 1px solid color-mix(in srgb, var(--accent)  25%, transparent); }
.badge--success { color: var(--success); background: var(--success-dim); border: 1px solid color-mix(in srgb, var(--success) 25%, transparent); }
.badge--warning { color: var(--warning); background: var(--warning-dim); border: 1px solid color-mix(in srgb, var(--warning) 25%, transparent); }
.badge--danger  { color: var(--danger);  background: var(--danger-dim);  border: 1px solid color-mix(in srgb, var(--danger)  25%, transparent); }
.badge--mono    { color: var(--text-dim); background: var(--bg-tint); border: 1px solid var(--border); }
```

---

### 5.4 — Section Structure

```html
<section class="section" id="section-id" aria-labelledby="section-heading">
  <div class="section__label" aria-hidden="true">01 — Architecture</div>
  <h2 id="section-heading">How the system <em>fits together</em></h2>
  <p class="section__lead">
    One or two sentences introducing this section. Keep under 80 words.
  </p>

  <!-- Content goes here -->

</section>
```

```css
.section {
  margin-bottom: 72px;
  scroll-margin-top: 60px;   /* offset for sticky nav */
}
.section__label {
  font-family: var(--font-mono);
  font-size: 10px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 2.5px;
  color: var(--accent);
  margin-bottom: 12px;
  display: flex;
  align-items: center;
  gap: 10px;
}
.section__label::after {
  content: '';
  flex: 1;
  height: 1px;
  background: var(--border);
}
/* h2 already in Typography Scale */
.section__lead {
  font-size: 17px;
  color: var(--text-dim);
  max-width: 680px;
  line-height: 1.65;
  margin-top: 14px;
}
```

---

### 5.5 — Cards

```html
<!-- Basic card -->
<div class="card">
  <h3>Card Title</h3>
  <p>Card description — one to three sentences explaining the concept.</p>
</div>

<!-- Card grid -->
<div class="grid-2">
  <div class="card anim" style="--i:0"> ... </div>
  <div class="card anim" style="--i:1"> ... </div>
  <div class="card anim" style="--i:2"> ... </div>
  <div class="card anim" style="--i:3"> ... </div>
</div>

<!-- Highlighted card (accent-border) -->
<div class="card card--accent"> ... </div>

<!-- Success / warning / danger tinted cards -->
<div class="card card--success"> ... </div>
<div class="card card--warning"> ... </div>
<div class="card card--danger"> ... </div>
```

```css
.card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 22px 24px;
  transition: border-color 0.2s, box-shadow 0.2s;
}
.card:hover {
  border-color: var(--border-hi);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.06);
}
.card h3 { margin-bottom: 8px; }
.card p  { font-size: 14.5px; color: var(--text-dim); }

.card--accent  { border-left: 3px solid var(--accent);  background: var(--accent-dim);  }
.card--success { border-left: 3px solid var(--success); background: var(--success-dim); }
.card--warning { border-left: 3px solid var(--warning); background: var(--warning-dim); }
.card--danger  { border-left: 3px solid var(--danger);  background: var(--danger-dim);  }

/* Grid helpers */
.grid-2 { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 16px; margin-top: 24px; }
.grid-3 { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 14px; margin-top: 24px; }
.grid-4 { display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 12px; margin-top: 20px; }
```

---

### 5.6 — Code Blocks

```html
<div class="code-block">
  <div class="code-block__header">
    <span class="code-block__lang">JavaScript</span>
    <span class="code-block__file">src/index.js</span>
  </div>
  <pre><code>// Your code here
const example = 'use the .ck .cs .cc .ca spans for syntax';
function hello(name) {
  return `Hello, ${name}!`;
}</code></pre>
</div>

<!-- Syntax highlight spans (inline, no library needed) -->
<!-- .ck = keyword    .cs = string    .cc = comment    .ca = accent/function -->
<pre><code><span class="ck">const</span> name = <span class="cs">'value'</span>;  <span class="cc">// comment</span>
<span class="ca">myFunction</span>(<span class="cs">'arg'</span>);</code></pre>
```

```css
.code-block {
  background: var(--code-bg);
  border-radius: 10px;
  overflow: hidden;
  margin-top: 16px;
  border: 1px solid rgba(255, 255, 255, 0.06);
}
.code-block__header {
  background: rgba(255, 255, 255, 0.04);
  border-bottom: 1px solid rgba(255, 255, 255, 0.06);
  padding: 10px 18px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.code-block__lang {
  font-family: var(--font-mono);
  font-size: 10px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 1.5px;
  color: rgba(200, 218, 240, 0.4);
}
.code-block__file {
  font-family: var(--font-mono);
  font-size: 11px;
  color: rgba(200, 218, 240, 0.3);
}
.code-block pre {
  padding: 20px 18px;
  margin: 0;
  font-family: var(--font-mono);
  font-size: 13.5px;
  line-height: 1.7;
  color: var(--code-text);
  white-space: pre-wrap;
  overflow-x: auto;
}
/* Syntax tokens */
.ck { color: var(--code-accent); }
.cs { color: var(--code-string); }
.cc { color: var(--code-comment); font-style: italic; }
.ca { color: var(--code-text); opacity: 0.85; }
```

---

### 5.7 — Comparison Table

```html
<div class="table-wrap">
  <table class="compare-table">
    <thead>
      <tr>
        <th>Feature</th>
        <th>Option A</th>
        <th class="col--hi">Option B (Recommended)</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Dark Mode</td>
        <td><span class="cell--no">✕ None</span></td>
        <td><span class="cell--yes">✓ Automatic</span></td>
      </tr>
      <tr>
        <td>Performance</td>
        <td><span class="cell--yes">✓ Fast</span></td>
        <td><span class="cell--partial">~ Slightly larger</span></td>
      </tr>
    </tbody>
  </table>
</div>
```

```css
.table-wrap {
  margin-top: 24px;
  overflow-x: auto;
  border-radius: 12px;
  border: 1px solid var(--border);
}
.compare-table {
  width: 100%;
  border-collapse: collapse;
}
.compare-table thead tr { background: var(--bg-tint); }
.compare-table th {
  font-family: var(--font-mono);
  font-size: 10.5px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 1.5px;
  color: var(--text-dim);
  padding: 13px 20px;
  text-align: left;
  border-bottom: 1px solid var(--border);
}
.compare-table th.col--hi { color: var(--accent); }
.compare-table td {
  padding: 12px 20px;
  font-size: 14px;
  color: var(--text);
  border-bottom: 1px solid var(--border);
  vertical-align: top;
}
.compare-table tr:last-child td { border-bottom: none; }
.compare-table td:first-child { color: var(--text-dim); font-size: 13px; }
.compare-table tbody tr:hover  { background: var(--surface); }
.cell--yes     { color: var(--success); }
.cell--no      { color: var(--text-dim); opacity: 0.5; }
.cell--partial { color: var(--warning); }
```

---

### 5.8 — Callout / Note Boxes

```html
<!-- Information callout -->
<div class="callout callout--info">
  <span class="callout__icon">ℹ</span>
  <div>
    <strong>Note:</strong> Important contextual information the reader needs.
  </div>
</div>

<!-- Warning callout -->
<div class="callout callout--warning">
  <span class="callout__icon">⚠</span>
  <div>
    <strong>Warning:</strong> Something to be careful about.
  </div>
</div>

<!-- Success callout -->
<div class="callout callout--success">
  <span class="callout__icon">✓</span>
  <div>
    <strong>Tip:</strong> A helpful recommendation.
  </div>
</div>

<!-- Danger callout -->
<div class="callout callout--danger">
  <span class="callout__icon">✕</span>
  <div>
    <strong>Deprecated:</strong> Do not use this approach in new code.
  </div>
</div>
```

```css
.callout {
  display: flex;
  gap: 12px;
  align-items: flex-start;
  padding: 14px 18px;
  border-radius: 8px;
  font-size: 14.5px;
  line-height: 1.6;
  margin-top: 16px;
}
.callout__icon {
  font-size: 14px;
  flex-shrink: 0;
  margin-top: 1px;
}
.callout strong { font-weight: 600; }
.callout--info    { background: var(--accent-dim);  border: 1px solid color-mix(in srgb, var(--accent)  20%, transparent); color: var(--text); }
.callout--info    .callout__icon { color: var(--accent);  }
.callout--warning { background: var(--warning-dim); border: 1px solid color-mix(in srgb, var(--warning) 20%, transparent); color: var(--text); }
.callout--warning .callout__icon { color: var(--warning); }
.callout--success { background: var(--success-dim); border: 1px solid color-mix(in srgb, var(--success) 20%, transparent); color: var(--text); }
.callout--success .callout__icon { color: var(--success); }
.callout--danger  { background: var(--danger-dim);  border: 1px solid color-mix(in srgb, var(--danger)  20%, transparent); color: var(--text); }
.callout--danger  .callout__icon { color: var(--danger);  }
```

---

### 5.9 — Step / Process List

```html
<ol class="steps">
  <li class="step">
    <div class="step__number" aria-hidden="true">01</div>
    <div class="step__body">
      <h3>Install dependencies</h3>
      <p>Run <code>npm install</code> in the project root.</p>
    </div>
  </li>
  <li class="step">
    <div class="step__number" aria-hidden="true">02</div>
    <div class="step__body">
      <h3>Configure environment</h3>
      <p>Copy <code>.env.example</code> to <code>.env</code> and fill in values.</p>
    </div>
  </li>
</ol>
```

```css
.steps { list-style: none; display: flex; flex-direction: column; gap: 0; }
.step {
  display: flex;
  gap: 20px;
  padding: 24px 0;
  border-bottom: 1px solid var(--border);
  align-items: flex-start;
}
.step:last-child { border-bottom: none; }
.step__number {
  font-family: var(--font-mono);
  font-size: 11px;
  font-weight: 600;
  color: var(--accent);
  background: var(--accent-dim);
  border: 1px solid color-mix(in srgb, var(--accent) 25%, transparent);
  border-radius: 6px;
  padding: 4px 10px;
  flex-shrink: 0;
  margin-top: 2px;
}
.step__body h3 { margin-bottom: 6px; font-size: 17px; }
.step__body p  { font-size: 14.5px; color: var(--text-dim); }
```

---

### 5.10 — Definition / Property List

```html
<dl class="prop-list">
  <div class="prop-row">
    <dt class="prop-key">Type</dt>
    <dd class="prop-val"><code>string</code></dd>
  </div>
  <div class="prop-row">
    <dt class="prop-key">Default</dt>
    <dd class="prop-val"><code>'utf-8'</code></dd>
  </div>
  <div class="prop-row">
    <dt class="prop-key">Required</dt>
    <dd class="prop-val"><span class="cell--no">No</span></dd>
  </div>
  <div class="prop-row">
    <dt class="prop-key">Description</dt>
    <dd class="prop-val">The character encoding used when reading the file.</dd>
  </div>
</dl>
```

```css
.prop-list { display: flex; flex-direction: column; border: 1px solid var(--border); border-radius: 10px; overflow: hidden; margin-top: 16px; }
.prop-row  { display: flex; border-bottom: 1px solid var(--border); }
.prop-row:last-child { border-bottom: none; }
.prop-key  {
  font-family: var(--font-mono);
  font-size: 12px;
  font-weight: 600;
  color: var(--text-dim);
  background: var(--bg-tint);
  padding: 10px 16px;
  min-width: 120px;
  border-right: 1px solid var(--border);
  flex-shrink: 0;
}
.prop-val {
  font-size: 14px;
  color: var(--text);
  padding: 10px 16px;
  line-height: 1.5;
}
```

---

### 5.11 — Footer

```html
<footer class="footer" role="contentinfo">
  <span>Project Name · Documentation v1.0</span>
  <span>Built with care ✦</span>
</footer>
```

```css
.footer {
  margin-top: 80px;
  padding-top: 24px;
  border-top: 1px solid var(--border);
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 8px;
  font-family: var(--font-mono);
  font-size: 11px;
  color: var(--text-dim);
}
```

---

## 6. COMPLETE PAGE TEMPLATE

*This is the full skeleton. The agent fills in project content, chosen palette, and chosen fonts.*

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>[PROJECT NAME] — Documentation</title>

<!-- STEP 1: Replace with chosen Font Pair import string from Section 3 -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="FONT_IMPORT_URL_HERE" rel="stylesheet">

<style>
/* ══════════════════════════════════════
   STEP 2: Paste chosen Palette from Section 2
   (both :root and @media dark blocks)
══════════════════════════════════════ */

/* STEP 3: Paste font tokens from chosen Font Pair (Section 3) */
:root {
  --font-display: '...', Georgia, serif;
  --font-body:    '...', system-ui, sans-serif;
  --font-mono:    '...', Consolas, monospace;
}

/* STEP 4: Paste the complete CSS Foundation from Section 4 */

/* STEP 5: Paste component CSS from Section 5 (only those you use) */

/* ══════════════════════════════════════
   PROJECT-SPECIFIC OVERRIDES (optional)
══════════════════════════════════════ */
/* Add any extra rules here */

</style>
</head>
<body>

<div class="shell">

  <!-- NAV (paste component 5.1) -->
  <nav class="nav" role="navigation" aria-label="Page sections">
    <div class="nav__inner">
      <span class="nav__brand">[PROJECT NAME]</span>
      <!-- Add section links matching your sections below -->
      <a href="#overview">Overview</a>
      <a href="#setup">Setup</a>
      <a href="#api">API</a>
    </div>
  </nav>

  <!-- HERO (paste component 5.2) -->
  <header class="hero" role="banner">
    <div class="hero__eyebrow anim" style="--i:0">[Doc type] · [Version]</div>
    <h1 class="anim" style="--i:1">
      [Project name]<br><em>[Italic memorable phrase]</em>
    </h1>
    <p class="hero__sub anim" style="--i:2">[One sentence describing what this doc covers]</p>
    <div class="hero__meta anim" style="--i:3">
      <span class="badge badge--success">v[X.X.X]</span>
      <span class="badge badge--mono">Updated [DATE]</span>
    </div>
  </header>

  <!-- SECTION TEMPLATE (repeat for each section) -->
  <section class="section" id="[section-id]" aria-labelledby="[section-id]-heading">
    <div class="section__label" aria-hidden="true">01 — [Section Name]</div>
    <h2 id="[section-id]-heading">[Section <em>headline</em>]</h2>
    <p class="section__lead">[Intro paragraph]</p>

    <!-- Insert cards, tables, code blocks, callouts as needed -->

  </section>

  <!-- Repeat sections... -->

  <!-- FOOTER -->
  <footer class="footer" role="contentinfo">
    <span>[Project Name] · Documentation</span>
    <span>✦</span>
  </footer>

</div>

<!-- Optional: smooth scroll for nav -->
<script>
  document.querySelectorAll('.nav a[href^="#"]').forEach(a => {
    a.addEventListener('click', e => {
      e.preventDefault();
      document.querySelector(a.getAttribute('href'))?.scrollIntoView({ behavior: 'smooth' });
    });
  });
</script>

<!-- Optional: Mermaid diagrams (only add if diagrams needed) -->
<!--
<script type="module">
  import mermaid from 'https://cdn.jsdelivr.net/npm/mermaid@11/dist/mermaid.esm.min.mjs';
  const dark = matchMedia('(prefers-color-scheme: dark)').matches;
  mermaid.initialize({
    startOnLoad: true,
    theme: 'base',
    themeVariables: {
      fontFamily: getComputedStyle(document.documentElement).getPropertyValue('--font-body').trim(),
      primaryColor:       dark ? '#1c3050' : '#f7f3eb',
      primaryBorderColor: dark ? '#d4a73a' : '#b8923a',
      primaryTextColor:   dark ? '#e4cf9c' : '#1c2a3a',
    }
  });
</script>
-->

</body>
</html>
```

---

## 7. QUALITY CHECKLIST

The agent must verify every item before returning the file:

### Visual Quality
- [ ] Background is layered — not a flat single colour
- [ ] Nav is sticky and has `backdrop-filter: blur()`
- [ ] Hero h1 uses `clamp()` for fluid sizing
- [ ] Hero h1 uses `<em>` for italic accent-coloured word
- [ ] Section labels have `::after` line rule extending to edge
- [ ] Cards have hover transitions on border and shadow
- [ ] Code blocks have a dark header strip + language label
- [ ] At least one `badge` variant is used in the hero

### Dark Mode
- [ ] Both `:root` and `@media (prefers-color-scheme: dark)` blocks present
- [ ] Every colour in CSS rules uses `var(--token)` — no raw hex in rules
- [ ] Dark bg is deep navy, not pure black
- [ ] Dark text is warm cream/gold, not pure white

### Typography
- [ ] Three font families imported and assigned to tokens
- [ ] Display font used only for headings
- [ ] Mono font used for nav links, labels, code, badges
- [ ] Section label is mono, uppercase, with letter-spacing

### Animation
- [ ] `.anim` class + `style="--i:N"` stagger on hero elements
- [ ] `@media (prefers-reduced-motion: reduce)` block present and correct

### Accessibility & Structure
- [ ] `<nav role="navigation">`, `<main>` or semantic wrapper, `<footer role="contentinfo">`
- [ ] Every `<section>` has `id` + `aria-labelledby` linking to its `<h2>`
- [ ] Sections have `scroll-margin-top` matching nav height
- [ ] Nav links use smooth scroll JavaScript
- [ ] `lang="en"` on `<html>`

### Technical
- [ ] Single self-contained file — all CSS and JS inline
- [ ] No external CSS frameworks (no Tailwind, Bootstrap, etc.)
- [ ] Only external CDN: Google Fonts + optional Mermaid
- [ ] `<link rel="preconnect">` tags present for Google Fonts
- [ ] `display=swap` on Fonts URL to prevent FOUT

---

## 8. QUICK REFERENCE — AGENT PROMPT TO USE

```
Read the full design.md file I'm attaching. Follow it exactly.

Project: [YOUR PROJECT NAME]
Palette: [A / B / C / D / E / Custom]
Font Pair: [A / B / C / D / E / Custom]

Sections to include:
1. [Section name] — [brief description of content]
2. [Section name] — [brief description of content]
3. [Section name] — [brief description of content]

Components needed: [e.g. code blocks, comparison table, step list, callouts]

Special requirements: [e.g. "include a Mermaid architecture diagram", "add a changelog table"]

Produce a single self-contained HTML file. Do not use any CSS framework.
Run through the Quality Checklist (Section 7) before returning.
```

---

*design.md — Premium HTML Documentation Design System*
*Palette options: A (Editorial Gold) · B (Blueprint Indigo) · C (Midnight Copper) · D (Forest Sage) · E (Obsidian Violet) · Custom*
*Font pairs: A (Instrument×Inter) · B (Fraunces×DM Sans) · C (DM Serif×Jakarta) · D (Space Grotesk×IBM Plex) · E (Playfair×Source Sans)*
