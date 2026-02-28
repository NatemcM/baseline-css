# Baseline CSS — Benchmarks

## File Size

| Metric | Baseline CSS | Tailwind CSS v4 (full) | Tailwind v4 (purged) |
|---|---|---|---|
| Uncompressed | **50 KB** | 2,413 KB | ~10-50 KB |
| Gzipped | **10 KB** | 190 KB | ~3-10 KB |
| Brotli | **8 KB** | 46 KB | ~2-5 KB |
| CSS Rules | ~620 | Varies | Varies |
| Build step | None | Required | Required |

Baseline ships the **entire framework** at 10 KB gzipped — comparable to a purged Tailwind build, but with zero build tooling.

## HTML Token Count (Characters in class/layout attributes)

Lower is better. Fewer tokens = faster LLM generation, smaller HTML, easier to read.

| Component | Baseline CSS | Tailwind CSS | Savings |
|---|---|---|---|
| Primary Button | 84 chars | 185 chars | **55%** fewer |
| Card | 33 chars | 64 chars | **48%** fewer |
| Form Input | 108 chars | 193 chars | **44%** fewer |
| Alert | 39 chars | 75 chars | **48%** fewer |
| Badge | 46 chars | 77 chars | **40%** fewer |
| Flex Row (centered) | 22 chars | 55 chars | **60%** fewer |
| **Average** | | | **~49% fewer** |

## Side-by-Side Comparison

### Primary Button

**Baseline CSS** (84 chars):
```html
<button class="px:4 py:2 bg:primary c:text-inverse r:md fw:500 t:sm tr:colors :hover>bg :focus>ring">
  Submit
</button>
```

**Tailwind CSS** (185 chars):
```html
<button class="px-4 py-2 bg-primary text-primary-foreground rounded-md font-medium text-sm transition-colors hover:bg-primary/90 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring">
  Submit
</button>
```

### Card

**Baseline CSS** (33 chars):
```html
<div class="p:6 bg:surface r:lg b:1 bc:border">
```

**Tailwind CSS** (64 chars):
```html
<div class="p-6 bg-card text-card-foreground rounded-lg border border-border">
```

### Layout (Flex Row, Centered)

**Baseline CSS** (22 chars):
```html
<div layout="row center g4">
```

**Tailwind CSS** (55 chars):
```html
<div class="flex flex-row items-center justify-center gap-4">
```

### Form Input

**Baseline CSS** (108 chars):
```html
<input class="px:3 py:2 bg:surface r:md b:1 bc:border t:sm c:text w:full outline:none tr:colors :focus>bc:text :focus>ring">
```

**Tailwind CSS** (193 chars):
```html
<input class="px-3 py-2 bg-background rounded-md border border-input text-sm text-foreground w-full outline-none transition-colors focus-visible:border-foreground focus-visible:ring-2 focus-visible:ring-ring">
```

## Why Fewer Tokens Matter

1. **LLM cost**: AI tools generate HTML by tokens. ~49% fewer class tokens = ~49% less generation cost and latency when building UI with AI.
2. **Readability**: Shorter classes are easier to scan. `bg:primary` vs `bg-primary text-primary-foreground`.
3. **No build step**: Baseline ships as a single CSS file. No PostCSS, no purging, no config. Link it and go.
4. **CSP compliance**: Zero inline styles required. Tailwind's arbitrary values (`bg-[#ff0]`) work, but Baseline achieves everything via pre-defined utilities.

## Architecture Comparison

| Feature | Baseline CSS | Tailwind CSS |
|---|---|---|
| Build step | None | Required (PostCSS/Vite) |
| CSP compliant | Yes (zero inline styles) | Partial (arbitrary values) |
| Layout system | `layout` attribute | Utility classes |
| Theming | `data-theme` composable | CSS variables + config |
| Dark mode | Composable theme | `dark:` variant |
| State hover | `:hover>bg` (generic) | `hover:bg-*` (per-class) |
| Accessibility themes | Built-in (reduce-motion, high-contrast, large-text) | Manual |
| Scoped themes | Any element via `data-theme` | Manual |
| File size (full) | 10 KB gzipped | 190 KB gzipped |
| File size (purged) | N/A (ship it all) | ~3-10 KB gzipped |
