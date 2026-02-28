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
- **LLM optimised** — ~60% fewer tokens than Tailwind for AI-assisted development

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
<nav layout="row center-between g4" class="px:6 py:3 bg:surface-raised sh:sm">
  <h1 class="t:xl fw:700 c:text">Logo</h1>
  <button class="px:4 py:2 bg:primary c:text-inverse r:md tr:colors :hover>bg:primary-hover">
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
| `bg` | background-color | `bg:primary`, `bg:surface-raised` |
| `c` | color | `c:text`, `c:text-muted`, `c:primary` |
| `t` | font-size | `t:sm`, `t:xl`, `t:3xl` |
| `fw` | font-weight | `fw:400`, `fw:600`, `fw:700` |
| `r` | border-radius | `r:sm`, `r:md`, `r:lg`, `r:full` |
| `sh` | box-shadow | `sh:sm`, `sh:md`, `sh:lg` |
| `b` | border | `b:1`, `bt:1`, `bb:1` |
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

Baseline uses semantic colour tokens instead of arbitrary palettes:

```css
:root {
  /* Brand */
  --primary         --primary-hover      --primary-active     --primary-subtle
  --secondary       --secondary-hover    --secondary-subtle
  --accent          --accent-hover       --accent-subtle

  /* Feedback */
  --success         --warning            --danger             --info

  /* Surfaces */
  --surface         --surface-raised     --surface-sunken

  /* Text */
  --text            --text-muted         --text-faint         --text-inverse

  /* Borders */
  --border          --border-subtle      --border-strong

  /* Neutrals (grey scale only) */
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
| `reduce-motion` | Zeroes all transition and animation durations |

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
| `@sm:` | 640px |
| `@md:` | 768px |
| `@lg:` | 1024px |
| `@xl:` | 1280px |

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

---

## State Variants

State variants use the `:state>domain:value` pattern:

```html
<button class="
  bg:primary c:text-inverse r:md px:4 py:2
  tr:colors
  :hover>bg:primary-hover
  :focus>ring:primary
  :active>scale:98
  :disabled>o:50
">
  Submit
</button>
```

The `>` reads naturally as "on hover, apply bg primary-hover".

| Prefix | Selector |
|--------|----------|
| `:hover>` | `:hover` |
| `:focus>` | `:focus-visible` |
| `:active>` | `:active` |
| `:disabled>` | `:disabled` |

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
<div class="flex flex-col gap-4 p-6 bg-white rounded-lg shadow-md hover:shadow-lg transition-shadow">
  <div class="flex items-center justify-between">
    <h3 class="text-lg font-semibold text-gray-900">Card Title</h3>
    <span class="text-sm text-gray-500">3 min ago</span>
  </div>
  <p class="text-gray-600 leading-relaxed">Card content goes here.</p>
  <div class="flex gap-2 pt-2 border-t border-gray-100">
    <button class="px-3 py-1.5 text-sm bg-blue-600 text-white rounded-md hover:bg-blue-700">Action</button>
    <button class="px-3 py-1.5 text-sm text-gray-600 rounded-md hover:bg-gray-100">Cancel</button>
  </div>
</div>
```

### Baseline
```html
<div layout="col g4" class="p:6 bg:surface-raised r:lg sh:md tr:shadow :hover>sh:lg">
  <div layout="row center-between">
    <h3 class="t:lg fw:600 c:text">Card Title</h3>
    <span class="t:sm c:text-muted">3 min ago</span>
  </div>
  <p class="c:text-muted lh:relaxed">Card content goes here.</p>
  <div layout="row g2" class="pt:2 bt:1 bc:border-subtle">
    <button class="px:3 py:1.5 t:sm bg:primary c:text-inverse r:md tr:colors :hover>bg:primary-hover">Action</button>
    <button class="px:3 py:1.5 t:sm c:text-muted r:md tr:colors :hover>bg:neutral-2">Cancel</button>
  </div>
</div>
```

**What's different:**
- Layout intent is immediately clear from the `layout` attribute
- Semantic colours (`bg:primary`) instead of arbitrary values (`bg-blue-600`)
- Compressed syntax reduces visual noise
- Dark mode works automatically — no `dark:` prefixes needed
- ~60% fewer tokens for LLM generation

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

**Background:** `bg:primary`, `bg:primary-subtle`, `bg:secondary`, `bg:accent`, `bg:success`, `bg:warning`, `bg:danger`, `bg:info`, `bg:surface`, `bg:surface-raised`, `bg:surface-sunken`, `bg:neutral-{1-9}`, `bg:transparent`

**Text:** `c:text`, `c:text-muted`, `c:text-faint`, `c:text-inverse`, `c:primary`, `c:secondary`, `c:accent`, `c:success`, `c:warning`, `c:danger`, `c:info`, `c:neutral-{1-9}`, `c:inherit`

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

**Border:** `b:0`, `b:1`, `b:2`, `bt:1`, `bb:1`, `bs:1`, `be:1`

**Border colour:** `bc:border`, `bc:border-subtle`, `bc:border-strong`, `bc:primary`, `bc:danger`, `bc:success`, `bc:transparent`

**Radius:** `r:none`, `r:sm`, `r:md`, `r:lg`, `r:xl`, `r:2xl`, `r:3xl`, `r:full`

### Shadows

`sh:none`, `sh:xs`, `sh:sm`, `sh:md`, `sh:lg`, `sh:xl`

### Sizing

**Width:** `w:full`, `w:auto`, `w:screen`, `w:min`, `w:max`, `w:fit`

**Max width:** `max-w:sm`, `max-w:md`, `max-w:lg`, `max-w:xl`, `max-w:full`, `max-w:prose`

**Height:** `h:full`, `h:auto`, `h:screen`, `h:min`, `h:fit`

**Min height:** `min-h:0`, `min-h:full`, `min-h:screen`

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

---

## Contributing

Baseline CSS is in early development. Contributions, feedback, and ideas are welcome.

---

## License

MIT