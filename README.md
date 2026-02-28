# Baseline CSS

A minimal, CSS-native utility framework. Zero build step. Fully CSP-compliant. Composable accessibility themes. Semantic design tokens.

```html
<!-- That's it. No build step. No config. -->
<link rel="stylesheet" href="baseline.css">
```

---

## Why Baseline?

Modern CSS has caught up. Nesting, `:has()`, `@container`, `@layer`, custom properties — the platform is powerful enough that your utility framework shouldn't need a build step, a config file, or a JIT compiler.

Baseline CSS is a single stylesheet that gives you:

- **Compressed utility syntax** — `p:4 bg:primary r:lg` instead of `p-4 bg-blue-600 rounded-lg`
- **Layout attributes** — `layout="row center-between g4"` reads like a design spec
- **Semantic colours** — `primary`, `secondary`, `accent` instead of arbitrary `blue-500` palettes
- **Composable themes** — `data-theme="dark high-contrast"` with zero class pollution
- **CSP compliance** — No inline styles. Enterprise-ready out of the box.
- **Generic state variants** — `:hover>bg` automatically uses the right hover colour for any semantic `bg:*`
- **LLM optimised** — ~49% fewer tokens than Tailwind for AI-assisted development

---

## Benchmarks

| Metric | Baseline CSS | Tailwind CSS v4 |
|---|---|---|
| Full file (gzipped) | **10 KB** | 190 KB (full) / ~3-10 KB (purged) |
| Build step | None | Required |
| CSP compliant | Yes | Partial |
| Avg HTML tokens | **~49% fewer** | Baseline |

| Component | Baseline | Tailwind | Savings |
|---|---|---|---|
| Primary Button | 84 chars | 185 chars | **55%** |
| Card | 33 chars | 64 chars | **48%** |
| Form Input | 108 chars | 193 chars | **44%** |
| Flex Row (centered) | 22 chars | 55 chars | **60%** |

See [BENCHMARKS.md](BENCHMARKS.md) for full side-by-side comparisons.

---

## Quick Start

### CDN
```html
<link rel="stylesheet" href="https://unpkg.com/baseline-css@latest/baseline.css">
```

### Download
Drop `baseline.css` into your project and link it:
```html
<link rel="stylesheet" href="/css/baseline.css">
```

### npm
```bash
npm install baseline-css
```
```js
import 'baseline-css/baseline.css';
```

---

## Core Concepts

### Two-Layer Styling

Baseline separates **structure** from **style**:

```html
<!-- layout attribute = structural composition -->
<!-- classes = visual properties -->
<nav layout="row center-between g4" class="px:6 py:3 bg:surface bb:1 bc:border-subtle">
  <h1 class="t:sm fw:600 c:text">Logo</h1>
  <button class="px:4 py:2 bg:text c:surface r:md fw:500 t:sm tr:colors :hover>o:90 :focus>ring">
    Sign Up
  </button>
</nav>
```

The `layout` attribute tells you what the element **does** spatially. The classes tell you what it **looks like**. No more decoding `flex items-center justify-between` to understand layout intent.

### Compressed Utility Syntax

Every utility class follows the `domain:value` pattern:

| Domain | Property | Example |
|--------|----------|---------|
| `p` | padding | `p:4`, `px:6`, `py:2` |
| `m` | margin | `m:4`, `mx:auto`, `mt:6` |
| `bg` | background-color | `bg:primary`, `bg:surface`, `bg:text` |
| `c` | color | `c:text`, `c:text-muted`, `c:surface` |
| `t` | font-size | `t:sm`, `t:xl`, `t:3xl` |
| `fw` | font-weight | `fw:400`, `fw:600`, `fw:700` |
| `r` | border-radius | `r:sm`, `r:md`, `r:lg`, `r:full` |
| `sh` | box-shadow | `sh:sm`, `sh:md`, `sh:lg` |
| `b` | border | `b:1`, `bt:1`, `bb:1` |
| `bc` | border-color | `bc:border`, `bc:primary`, `bc:text` |
| `o` | opacity | `o:0`, `o:50`, `o:100` |
| `tr` | transition | `tr:all`, `tr:colors`, `tr:shadow` |
| `w` / `h` | width / height | `w:full`, `h:screen` |
| `z` | z-index | `z:dropdown`, `z:modal`, `z:toast` |

See the full [domain reference](#domain-reference) below.

### Layout Attribute

The `layout` attribute uses space-separated tokens for flex, grid, alignment, and gap:

```html
<!-- Flex row, vertically centred, space-between, gap of 1rem -->
<div layout="row center-between g4">

<!-- Grid, 3 columns, gap of 1.5rem -->
<div layout="grid cols-3 g6">

<!-- Column stack, items stretched, gap of 0.5rem -->
<div layout="col stretch g2">

<!-- Centred container with max-width -->
<div layout="container">
```

**Alignment tokens** combine align-items and justify-content into a single readable token:

| Token | align-items | justify-content |
|-------|------------|-----------------|
| `center` | center | center |
| `center-between` | center | space-between |
| `center-start` | center | flex-start |
| `center-end` | center | flex-end |
| `start` | flex-start | flex-start |
| `start-between` | flex-start | space-between |
| `end` | flex-end | flex-end |
| `stretch` | stretch | — |
| `baseline` | baseline | — |

---

## Base Size Scaling

The `--base-size` token controls the root `font-size`. Since all values use `rem`, changing this single token scales the entire framework:

```css
:root {
  --base-size: 100%;   /* default: 1rem = 16px */
  --base-size: 112.5%; /* larger:  1rem = 18px */
  --base-size: 87.5%;  /* smaller: 1rem = 14px */
}
```

This lets users scale the entire UI up or down by changing one variable.

---

## Theming

### Design Tokens

Everything in Baseline flows from CSS custom properties. Customise your design by overriding them:

```css
:root {
  --primary: oklch(0.55 0.22 280);
  --primary-hover: oklch(0.48 0.22 280);
  --font-sans: 'Inter', system-ui, sans-serif;
  --r-md: 0.5rem;
  --s-4: 1.125rem;
}
```

No config files. No rebuild. Just CSS.

### Semantic Colours

Baseline uses semantic colour tokens instead of arbitrary palettes. Every semantic colour has a full family of state variants:

```css
:root {
  /* Brand — each has base, hover, active, subtle */
  --primary         --primary-hover      --primary-active     --primary-subtle
  --secondary       --secondary-hover    --secondary-active   --secondary-subtle
  --accent          --accent-hover       --accent-active      --accent-subtle

  /* Feedback — same pattern */
  --success         --success-hover      --success-active     --success-subtle
  --warning         --warning-hover      --warning-active     --warning-subtle
  --danger          --danger-hover       --danger-active      --danger-subtle
  --info            --info-hover         --info-active        --info-subtle

  /* Surfaces */
  --surface         --surface-raised     --surface-sunken     --surface-overlay

  /* Text */
  --text            --text-muted         --text-faint         --text-inverse

  /* Borders */
  --border          --border-subtle      --border-strong

  /* Neutrals (grey scale) */
  --neutral-1 through --neutral-9
}
```

This means changing your brand colour updates every button, link, and accent across your entire site — by changing one variable.

### Dark Mode

Dark mode is handled by reassigning variables, not adding class prefixes:

```html
<html data-theme="dark">
```

That's it. Every component automatically adapts. No `dark:bg-gray-900 dark:text-white` scattered across your templates.

Toggle with JS:
```js
const root = document.documentElement;
root.dataset.theme = root.dataset.theme === 'dark' ? 'light' : 'dark';
```

Baseline also respects `prefers-color-scheme: dark` automatically when no `data-theme` is set.

### Scoped Themes

Because themes cascade through CSS custom properties, you can scope them to any element:

```html
<body data-theme="light">
  <!-- Light-themed page -->

  <section data-theme="dark" class="bg:surface p:8 r:lg">
    <!-- This section is dark-themed -->
    <p class="c:text">This text adapts automatically.</p>
  </section>
</body>
```

### Composable Accessibility Themes

Themes stack via space-separated values. Each theme only touches the variables it cares about, so they compose without conflicts:

```html
<!-- Stack as many as you need -->
<html data-theme="dark high-contrast large-text reduce-motion">
```

| Theme | Effect |
|-------|--------|
| `dark` | Dark colour scheme |
| `high-contrast` | Stronger contrast ratios, heavier borders, bolder focus rings |
| `large-text` | Scaled-up typography for low vision |
| `reduce-motion` | Pauses all animations via `--anim-state` token |

Build a preferences panel:
```js
function setThemes(themes) {
  document.documentElement.dataset.theme = themes.join(' ');
  localStorage.setItem('user-themes', JSON.stringify(themes));
}

// Restore on load
const saved = JSON.parse(localStorage.getItem('user-themes') || '[]');
if (saved.length) document.documentElement.dataset.theme = saved.join(' ');
```

---

## Responsive Design

Responsive variants use the `@` prefix, mirroring CSS at-rules:

| Prefix | Min Width |
|--------|-----------|
| `@sm:` | 640px (40rem) |
| `@md:` | 768px (48rem) |
| `@lg:` | 1024px (64rem) |
| `@xl:` | 1280px (80rem) |
| `@2xl:` | 1536px (96rem) |

Works in both layout attributes and utility classes:

```html
<!-- Stack on mobile, row on tablet -->
<div layout="col @md:row center g4 @md:g8">

  <!-- Smaller text on mobile, larger on desktop -->
  <h1 class="t:2xl @lg:t:4xl fw:700">Responsive Heading</h1>

  <!-- Adjust padding at breakpoints -->
  <div class="p:4 @md:p:6 @lg:p:8">
    Content
  </div>
</div>
```

Responsive variants are available for: display, spacing (p/px/py/mb/mt/mx), typography, text-align, width, max-width, order, and all layout attributes (grid cols, gap, direction, spans).

---

## State Variants

### Generic State Pattern

Semantic `bg:*` utilities set private CSS variables for their hover, active, and ring colours. Generic state classes read these variables, so **one class works for every colour**:

```html
<!-- :hover>bg automatically uses danger-hover because bg:danger set it -->
<button class="bg:danger c:text-inverse r:md px:4 py:2 tr:colors :hover>bg :active>bg :focus>ring">
  Delete
</button>
```

This means adding a new colour to your design system automatically gets hover, active, and focus states — no extra state classes needed.

The same pattern applies to shadows — each `sh:*` utility sets `--_sh-hover` to the next elevation:

```html
<!-- Automatically elevates: xs→sm, sm→md, md→lg, lg→xl -->
<div class="sh:md :hover>sh">
```

### How It Works

Each semantic `bg:*` utility sets private custom properties:

```css
.bg\:primary {
  background-color: var(--primary);
  --_bg-hover: var(--primary-hover);
  --_bg-active: var(--primary-active);
  --_ring: var(--primary);
}

/* One class covers ALL semantic colours */
.\:hover\>bg:hover { background-color: var(--_bg-hover); }
.\:active\>bg:active { background-color: var(--_bg-active); }
.\:focus\>ring:focus-visible {
  outline: var(--focus-ring-width) solid var(--_ring);
  outline-offset: var(--focus-ring-offset);
}
```

### Explicit Overrides

For non-semantic colours or when you need a specific target, explicit variants still work:

```html
<!-- Neutral bg doesn't have state vars, use explicit -->
<button class="bg:surface :hover>bg:neutral-2 :focus>ring:primary">Outline</button>

<!-- Override the generic hover with a specific colour -->
<button class="bg:primary :hover>bg:danger">Custom Hover</button>
```

| Generic | Reads from | Set by |
|---------|-----------|--------|
| `:hover>bg` | `--_bg-hover` | `bg:primary`, `bg:danger`, etc. |
| `:active>bg` | `--_bg-active` | `bg:primary`, `bg:danger`, etc. |
| `:focus>ring` | `--_ring` | `bg:*` (defaults to `--focus-ring` / primary) |
| `:hover>sh` | `--_sh-hover` | `sh:xs`, `sh:sm`, `sh:md`, `sh:lg`, `sh:xl` |

### Explicit State Variants

| Prefix | Selector |
|--------|----------|
| `:hover>` | `:hover` |
| `:focus>` | `:focus-visible` |
| `:active>` | `:active` |
| `:disabled>` | `:disabled` |

Available explicit variants: `:hover>bg:neutral-2`, `:hover>bg:neutral-3`, `:hover>c:text`, `:hover>c:text-muted`, `:hover>c:primary`, `:hover>o:90`, `:hover>scale:105`, `:hover>td:underline`, `:hover>td:none`, `:focus>bc:text`, `:focus>bc:primary`, `:active>scale:98`, `:disabled>o:50`, and more.

---

## Animations

Built-in animation utilities that respect the `reduce-motion` theme:

```html
<div class="anim:spin">   <!-- 360° rotation -->
<div class="anim:pulse">  <!-- Scale pulse -->
<div class="anim:bounce"> <!-- Bounce up/down -->
<div class="anim:fade-in"> <!-- Fade in from transparent -->
<div class="anim:slide-up"> <!-- Slide up from below -->
<div class="anim:shake">  <!-- Horizontal shake -->
```

All animations use `animation-play-state: var(--anim-state)`. The `reduce-motion` theme sets `--anim-state: paused`, instantly freezing all animations without JavaScript.

---

## CSP Compliance

Baseline is **fully CSP-compliant at every tier**. The entire framework is an external stylesheet — no inline styles are generated or required.

For arbitrary one-off values, an optional Vite plugin (coming soon) compiles patterns like `w:[503px]` into real CSS classes at build time, maintaining strict CSP compliance:

```js
// vite.config.js
import { baselinePlugin } from 'baseline-css/vite';

export default {
  plugins: [baselinePlugin()]
};
```

This makes Baseline a better fit for enterprise environments with strict security policies than frameworks that rely on inline styles or `style-src 'unsafe-inline'`.

---

## Comparison

A card component in Tailwind vs Baseline:

### Tailwind
```html
<div class="flex flex-col gap-4 p-6 bg-card text-card-foreground rounded-lg border border-border">
  <div class="flex items-center justify-between">
    <h3 class="text-sm font-semibold text-foreground">Card Title</h3>
    <span class="text-xs text-muted-foreground">3 min ago</span>
  </div>
  <p class="text-sm text-muted-foreground leading-relaxed">Card content goes here.</p>
  <div class="flex gap-2 pt-3 border-t border-border">
    <button class="px-3 py-1 text-xs bg-primary text-primary-foreground rounded-md transition-colors hover:bg-primary/90">Action</button>
    <button class="px-3 py-1 text-xs text-muted-foreground rounded-md hover:bg-accent">Cancel</button>
  </div>
</div>
```

### Baseline
```html
<div layout="col g3" class="p:6 bg:surface r:lg b:1 bc:border">
  <div layout="row center-between">
    <h4 class="t:sm fw:600 c:text">Card Title</h4>
    <span class="t:xs c:text-faint">3 min ago</span>
  </div>
  <p class="t:sm c:text-muted lh:relaxed">Card content goes here.</p>
  <div layout="row g2" class="pt:3 bt:1 bc:border-subtle">
    <button class="px:3 py:1 t:xs bg:text c:surface r:md tr:colors :hover>o:90">Action</button>
    <button class="px:3 py:1 t:xs c:text-muted r:md tr:colors :hover>bg:neutral-2">Cancel</button>
  </div>
</div>
```

**What's different:**
- Layout intent is immediately clear from the `layout` attribute
- Semantic colours (`bg:primary`) instead of arbitrary values (`bg-blue-600`)
- Generic state variants (`:hover>bg`) instead of per-colour classes
- Compressed syntax reduces visual noise
- Dark mode works automatically — no `dark:` prefixes needed
- ~49% fewer tokens for LLM generation

---

## Domain Reference

### Spacing (Padding & Margin)

Directional prefixes: `p` (all), `px` (inline), `py` (block), `pt` (top), `pb` (bottom), `ps` (start), `pe` (end). Same pattern for `m` (margin).

Values reference the spacing scale: `0`, `0.5`, `1`, `1.5`, `2`, `3`, `4`, `5`, `6`, `8`, `10`, `12`, `16`

```html
<div class="p:6 mx:auto mt:8">
<div class="px:4 py:2">
```

### Colours

**Background:** `bg:primary`, `bg:primary-subtle`, `bg:secondary`, `bg:accent`, `bg:success`, `bg:warning`, `bg:danger`, `bg:info`, `bg:surface`, `bg:surface-raised`, `bg:surface-sunken`, `bg:text`, `bg:neutral-{1-9}`, `bg:transparent`

**Text:** `c:text`, `c:text-muted`, `c:text-faint`, `c:text-inverse`, `c:surface`, `c:primary`, `c:secondary`, `c:accent`, `c:success`, `c:warning`, `c:danger`, `c:info`, `c:neutral-{1-9}`, `c:inherit`

**Border:** `bc:border`, `bc:border-subtle`, `bc:border-strong`, `bc:text`, `bc:primary`, `bc:secondary`, `bc:accent`, `bc:success`, `bc:warning`, `bc:danger`, `bc:info`, `bc:transparent`

### Typography

**Size:** `t:xs` (0.75rem), `t:sm` (0.875rem), `t:base` (1rem), `t:lg` (1.125rem), `t:xl` (1.25rem), `t:2xl` (1.5rem), `t:3xl` (1.875rem), `t:4xl` (2.25rem), `t:5xl` (3rem)

**Weight:** `fw:100` through `fw:900`

**Family:** `ff:sans`, `ff:serif`, `ff:mono`

**Line height:** `lh:tight`, `lh:snug`, `lh:base`, `lh:relaxed`, `lh:loose`

**Letter spacing:** `ls:tight`, `ls:normal`, `ls:wide`, `ls:wider`

**Align:** `ta:left`, `ta:center`, `ta:right`, `ta:justify`

**Decoration:** `td:none`, `td:underline`, `td:line-through`

**Transform:** `tt:upper`, `tt:lower`, `tt:cap`

**Utilities:** `truncate`, `line-clamp-2`, `line-clamp-3`

### Borders

**Border:** `b:0`, `b:1`, `b:2`, `bt:1`, `bt:2`, `bb:1`, `bb:2`, `bs:1`, `bs:2`, `be:1`, `be:2`

**Radius:** `r:none`, `r:sm`, `r:md`, `r:lg`, `r:xl`, `r:2xl`, `r:3xl`, `r:full`

### Shadows

`sh:none`, `sh:xs`, `sh:sm`, `sh:md`, `sh:lg`, `sh:xl`

Each shadow utility sets `--_sh-hover` to the next level, so `:hover>sh` auto-elevates.

### Sizing

**Width:** `w:full`, `w:auto`, `w:screen`, `w:min`, `w:max`, `w:fit`, `w:half`

**Max width:** `max-w:sm`, `max-w:md`, `max-w:lg`, `max-w:xl`, `max-w:full`, `max-w:prose`

**Height:** `h:full`, `h:auto`, `h:screen`, `h:min`, `h:fit`

**Min height:** `min-h:0`, `min-h:full`, `min-h:screen`

**Fixed sizes:** `size:4`, `size:5`, `size:6`, `size:8`, `size:10`, `size:12`, `size:16`

### Animations

`anim:spin`, `anim:pulse`, `anim:bounce`, `anim:fade-in`, `anim:slide-up`, `anim:shake`

All respect `--anim-state` (paused in `reduce-motion` theme).

### Effects

**Opacity:** `o:0`, `o:5`, `o:10`, `o:20`, `o:25`, `o:30`, `o:40`, `o:50`, `o:60`, `o:70`, `o:75`, `o:80`, `o:90`, `o:100`

**Transitions:** `tr:none`, `tr:all`, `tr:colors`, `tr:shadow`, `tr:opacity`, `tr:transform`

**Duration:** `dur:fast`, `dur:base`, `dur:slow`, `dur:slower`

**Scale:** `scale:95`, `scale:98`, `scale:100`, `scale:102`, `scale:105`, `scale:110`

### Layout Attribute Tokens

**Direction:** `row`, `col`, `grid`, `inline`, `hidden`

**Alignment:** `center`, `center-between`, `center-around`, `center-evenly`, `center-start`, `center-end`, `start`, `start-between`, `end`, `end-between`, `stretch`, `baseline`

**Wrap:** `wrap`, `nowrap`

**Gap:** `g0`, `g0.5`, `g1`, `g1.5`, `g2`, `g3`, `g4`, `g5`, `g6`, `g8`, `g10`, `g12`, `g16`

**Grid:** `cols-1` through `cols-6`, `cols-12`, `cols-auto`, `span-2` through `span-6`, `span-full`

**Flex child:** `fill`, `grow`, `shrink-0`, `self-start`, `self-center`, `self-end`, `self-stretch`

**Container:** `container`, `container-sm`, `container-md`, `container-lg`

**Position:** `relative`, `absolute`, `fixed`, `sticky`

**Overflow:** `clip`, `scroll`, `scroll-x`, `scroll-y`

---

## Browser Support

Baseline CSS uses modern CSS features supported in all evergreen browsers:

- CSS Custom Properties
- `@layer`
- `oklch()` colour space
- Attribute selectors
- `100dvh` dynamic viewport units
- `@media (width >= ...)` range syntax

**Supported:** Chrome 111+, Firefox 113+, Safari 16.4+, Edge 111+

---

## Philosophy

Baseline CSS exists because:

1. **CSS has evolved.** The platform handles most of what utility frameworks abstract away. A modern framework should leverage CSS, not replace it.

2. **Class soup is a real problem.** Co-location is good. Illegible 200-character class strings are not. Compressed syntax and layout attributes solve this.

3. **Naming colours `blue-600` is an anti-pattern.** Semantic tokens (primary, secondary, accent) force better design systems and make theming trivial.

4. **Accessibility shouldn't be an afterthought.** Composable themes for high contrast, large text, and reduced motion are built into the architecture.

5. **Build steps should be optional.** A `<link>` tag should be enough.

6. **LLMs write a lot of code now.** Token efficiency matters for cost, speed, and context window limits.

7. **State variants should be smart.** Generic `:hover>bg` that reads from the base colour's family is better than writing N explicit hover classes per colour.

---

## Contributing

Baseline CSS is in early development. Contributions, feedback, and ideas are welcome.

---

## License

MIT
