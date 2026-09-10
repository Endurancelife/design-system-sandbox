# [Company Name] Design System

> Reference file for AI tools (Claude, ChatGPT, v0, Cursor, etc.) generating pages, components, or code for our site.
> Source of truth. If output doesn't match this file, the file wins — flag the conflict, don't guess.
> Tokens below are the real exported values from our tweakcn theme (last updated 2026-09-10).

## How to use this file
When asking an LLM to build a page or component, paste or attach this whole file as context, then give the specific request. Example prompt: "Using the attached design system, build a product listing page with a filter sidebar and card grid."

---

## 1. Overview

- **Brand personality:** [e.g. confident, approachable, no-nonsense — 3-5 adjectives]
- **Primary audience:** [who uses the site]
- **Current stack:** PHP templating (legacy), migrating toward Next.js/React over time. Sandbox testing environment is plain HTML/CSS on GitHub Pages.
- **Palette character:** near-black primary with a light gray secondary and a single red-orange accent — restrained, monochrome-plus-one-accent.
- **Output format we want right now:** semantic HTML + CSS using the variables below, NOT React/JSX, unless explicitly asked for a React component.

---

## 2. Design Tokens

> Source: tweakcn export. Colors use the `oklch()` format (lightness, chroma, hue) rather than hex — treat the values as opaque tokens, not something to hand-edit by eye. Full Tailwind v4 build version of this file (with `@theme inline`, `@apply`, etc.) is kept separately for the future Next.js migration; the version below is the plain-CSS subset used in the current sandbox and on the PHP site.

### Colors — light mode (`:root`)
```css
:root {
  --background: oklch(1.0000 0 0);
  --foreground: oklch(0 0 0);
  --card: oklch(1.0000 0 0);
  --card-foreground: oklch(0 0 0);
  --primary: oklch(0.1448 0 0);            /* near-black — primary actions */
  --primary-foreground: oklch(1.0000 0 0);
  --secondary: oklch(0.9672 0 0);          /* light gray */
  --secondary-foreground: oklch(0.1448 0 0);
  --muted: oklch(0.9672 0 0);
  --muted-foreground: oklch(0.5103 0 0);
  --accent: oklch(0.5394 0.1903 26.4247);  /* red-orange accent */
  --accent-foreground: oklch(1.0000 0 0);
  --destructive: oklch(0.6280 0.2577 29.2339);
  --destructive-foreground: oklch(1.0000 0 0);
  --border: oklch(0.9219 0 0);
  --ring: oklch(0.1448 0 0);
}
```

### Colors — dark mode (`.dark`)
```css
.dark {
  --background: oklch(0.1448 0 0);
  --foreground: oklch(1.0000 0 0);
  --card: oklch(0.1822 0 0);
  --card-foreground: oklch(1.0000 0 0);
  --primary: oklch(1.0000 0 0);
  --primary-foreground: oklch(0.1448 0 0);
  --secondary: oklch(0.2178 0 0);
  --secondary-foreground: oklch(1.0000 0 0);
  --muted: oklch(0.2178 0 0);
  --muted-foreground: oklch(0.7118 0.0129 286.0665);
  --accent: oklch(0.6280 0.2577 29.2339);
  --accent-foreground: oklch(1.0000 0 0);
  --border: oklch(0.2686 0 0);
  --ring: oklch(1.0000 0 0);
}
```

### Typography
```css
--font-sans: Inter, system-ui, sans-serif;   /* body + UI */
--font-serif: Georgia, serif;                /* editorial use only, if any */
--font-mono: 'JetBrains Mono', monospace;    /* code, tabular data */
--tracking-normal: -0.02em;                  /* base letter-spacing */
```
**Type scale (sizes for h1/h2/body/etc.) is not yet defined** — tweakcn/shadcn doesn't set this for you by default. Add real values here once decided, rather than letting an LLM invent its own scale.

### Spacing
```css
--spacing: 0.25rem;  /* base unit — shadcn's spacing scale multiplies this (1 = 0.25rem, 2 = 0.5rem, 4 = 1rem, etc.) */
```
A fuller spacing scale (specific values for gaps, padding, section spacing) is not yet defined beyond this base unit — add as real components get built.

### Radius & Shadows
```css
--radius: 0.25rem;   /* base radius — components derive sm/md/lg/xl from this */
--shadow-sm: 0px 4px 10px 0px hsl(0 0% 0% / 0.10), 0px 1px 2px -1px hsl(0 0% 0% / 0.10);
--shadow-lg: 0px 4px 10px 0px hsl(0 0% 0% / 0.10), 0px 4px 6px -1px hsl(0 0% 0% / 0.10);
```

### Breakpoints
```css
/* mobile-first — not yet customized, using conventional defaults */
--bp-sm: 640px;
--bp-md: 768px;
--bp-lg: 1024px;
--bp-xl: 1280px;
```

---

## 3. Component Patterns

> For each component: what it's for, when to use it, and a real code example using the tokens above. Add new components here as they're built.
### Page Heading

**Use for:** the text-focused header of a hero section — pre-heading label, title, description, and action buttons.

​html
<div class="page-heading">
  <span class="page-heading__tagline">New — sandbox live</span>
  <h1 class="page-heading__title">Design system test</h1>
  <p class="page-heading__body">Supporting description text goes here.</p>
  <div class="page-heading__actions">
    <button class="btn btn--primary">Get started</button>
    <button class="btn btn--secondary">Learn more</button>
  </div>
</div>
​

​css
.page-heading { max-width: 48rem; display: flex; flex-direction: column; gap: calc(var(--spacing) * 3); }
.page-heading__tagline { display: inline-flex; align-items: center; width: fit-content; padding: calc(var(--spacing) * 1) calc(var(--spacing) * 3); background: var(--secondary); color: var(--secondary-foreground); border-radius: 999px; font-family: var(--font-sans); font-size: 0.8125rem; font-weight: 500; }
.page-heading__title { font-family: var(--font-sans); font-size: 2.75rem; font-weight: 500; letter-spacing: var(--tracking-normal); line-height: 1.1; color: var(--foreground); margin: 0; }
.page-heading__body { max-width: 36rem; font-family: var(--font-sans); font-size: 1.125rem; color: var(--muted-foreground); margin: 0; }
.page-heading__actions { display: flex; gap: calc(var(--spacing) * 1.5); margin-top: calc(var(--spacing) * 2); }
​

### Button

**Use for:** primary actions (submit, buy, continue). Use the secondary variant for lower-priority actions on the same screen — don't put two primary buttons side by side.

```html
<button class="btn btn--primary">Primary action</button>
<button class="btn btn--secondary">Secondary action</button>
```

```css
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: calc(var(--spacing) * 3) calc(var(--spacing) * 6);
  border-radius: var(--radius);
  font-family: var(--font-sans);
  font-weight: 500;
  font-size: 1rem;
  border: 1px solid transparent;
  cursor: pointer;
  transition: opacity 0.15s ease;
}
.btn--primary {
  background: var(--primary);
  color: var(--primary-foreground);
}
.btn--primary:hover { opacity: 0.85; }
.btn--secondary {
  background: transparent;
  color: var(--foreground);
  border-color: var(--border);
}
```

### Card

**Use for:** grouping related content in a grid (products, articles, features).

```html
<div class="card">
  <img src="..." alt="..." class="card__image" />
  <div class="card__body">
    <h3 class="card__title">Title</h3>
    <p class="card__description">Description text.</p>
  </div>
</div>
```

```css
.card {
  background: var(--card);
  color: var(--card-foreground);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  overflow: hidden;
  box-shadow: var(--shadow-sm);
}
.card__body { padding: calc(var(--spacing) * 4); }
.card__title { font-size: 1.125rem; font-weight: 500; margin-bottom: calc(var(--spacing) * 2); }
.card__description { color: var(--muted-foreground); font-size: 0.875rem; }
```

### [Add: Nav, Form inputs, Footer, etc. as you build them]

---

## 4. Layout Conventions

- Max content width: [e.g. 1280px, centered]
- Grid: [e.g. 12-column, gap based on `--spacing`]
- Standard page sections: header → hero/intro → main content → footer

---

## 5. Do's and Don'ts

**Do:**
- Use existing components/tokens above before inventing new colors, spacing, or radius values.
- Use semantic HTML (`<nav>`, `<button>`, `<article>`) — matters for SEO and eventual React conversion.
- Keep new components visually consistent with the ones defined here.
- Treat `oklch()` color values as opaque — copy them exactly, don't approximate with hex.

**Don't:**
- Introduce new one-off colors, font sizes, or spacing values outside the token list.
- Use inline styles — use the CSS variables/classes above.
- Generate React/JSX unless explicitly asked — default output is plain HTML/CSS for now.

---

## 6. Changelog
| Date | Change |
|------|--------|
| 2026-09-10 | Replaced placeholder tokens with real values exported from tweakcn (oklch colors, Inter/Georgia/JetBrains Mono fonts, 0.25rem base radius/spacing) |
| [earlier date] | Initial version |
