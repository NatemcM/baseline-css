<script>
	import { base } from '$app/paths';
	import CodeBlock from '$lib/components/CodeBlock.svelte';
</script>

<svelte:head>
	<title>Baseline CSS — The CSS framework LLMs actually understand</title>
</svelte:head>

<!-- Hero -->
<section layout="container" class="py:16 @md:py:24">
	<div layout="col g6" class="max-w:lg">
		<span class="px:3 py:1 t:xs fw:600 bg:primary-subtle c:primary r:full w:fit">v0.2.0</span>
		<h1 class="t:4xl @md:t:5xl fw:700 c:text lh:tight ls:tight">
			The CSS framework<br>
			<span class="c:primary">LLMs actually understand.</span>
		</h1>
		<p class="t:lg c:text-muted lh:relaxed max-w:prose">
			A minimal, CSS-native utility framework. Zero build step. Fully CSP-compliant.
			Semantic naming that reads like a design spec &mdash; and generates 49% fewer tokens than Tailwind.
		</p>
		<div layout="row g3 wrap">
			<a href="{base}/docs/getting-started"
				class="px:5 py:3 bg:primary c:text-inverse r:lg fw:600 t:sm td:none tr:colors :hover>bg :focus>ring">
				Get Started
			</a>
			<a href="https://github.com/NatemcM/baseline-css"
				class="px:5 py:3 bg:surface c:text r:lg fw:600 t:sm td:none b:1 bc:border tr:colors :hover>bg:neutral-2">
				GitHub
			</a>
		</div>
	</div>
</section>

<!-- Stats bar -->
<section class="bg:surface-sunken py:8 bt:1 bb:1 bc:border-subtle">
	<div layout="container">
		<div layout="row center-around wrap g6">
			<div layout="col center" class="ta:center">
				<span class="t:3xl fw:700 c:text">10 KB</span>
				<span class="t:sm c:text-muted">gzipped &mdash; full framework</span>
			</div>
			<div layout="col center" class="ta:center">
				<span class="t:3xl fw:700 c:text">1,758</span>
				<span class="t:sm c:text-muted">utility classes</span>
			</div>
			<div layout="col center" class="ta:center">
				<span class="t:3xl fw:700 c:text">49%</span>
				<span class="t:sm c:text-muted">fewer tokens than Tailwind</span>
			</div>
			<div layout="col center" class="ta:center">
				<span class="t:3xl fw:700 c:primary">Zero</span>
				<span class="t:sm c:text-muted">build step required</span>
			</div>
		</div>
	</div>
</section>

<!-- Quick start -->
<section layout="container" class="py:16">
	<div layout="col g8" class="max-w:lg">
		<div layout="col g3">
			<h2 class="t:2xl fw:700 c:text">Drop it in. Start building.</h2>
			<p class="t:base c:text-muted lh:relaxed">No PostCSS. No config file. No JIT compiler. One stylesheet.</p>
		</div>
		<CodeBlock code={'<link rel="stylesheet" href="https://unpkg.com/baseline-css@latest/baseline.css">'} lang="html" />
	</div>
</section>

<!-- Comparison -->
<section class="bg:surface-sunken py:16 bt:1 bb:1 bc:border-subtle">
	<div layout="container">
		<div layout="col g8" class="max-w:xl mx:auto">
			<div layout="col g3" class="ta:center">
				<h2 class="t:2xl fw:700 c:text">Tailwind vs Baseline</h2>
				<p class="t:base c:text-muted">Same component. Dramatically less noise.</p>
			</div>

			<div layout="grid @md:cols-2 g6">
				<div layout="col g2">
					<span class="t:xs fw:600 c:text-muted tt:upper ls:wide">Tailwind &mdash; 185 chars</span>
					<CodeBlock code={'<button class="px-4 py-2 bg-primary\n  text-primary-foreground rounded-md\n  font-medium text-sm transition-colors\n  hover:bg-primary/90\n  focus-visible:outline-none\n  focus-visible:ring-2\n  focus-visible:ring-ring">\n  Submit\n</button>'} />
				</div>
				<div layout="col g2">
					<span class="t:xs fw:600 c:primary tt:upper ls:wide">Baseline &mdash; 84 chars</span>
					<CodeBlock code={'<button class="px:4 py:2 bg:primary\n  c:text-inverse r:md fw:500 t:sm\n  tr:colors :hover>bg :focus>ring">\n  Submit\n</button>'} />
				</div>
			</div>

			<div layout="grid @md:cols-2 g6">
				<div layout="col g2">
					<span class="t:xs fw:600 c:text-muted tt:upper ls:wide">Tailwind &mdash; 55 chars</span>
					<CodeBlock code={'<div class="flex flex-row items-center\n  justify-center gap-4">'} />
				</div>
				<div layout="col g2">
					<span class="t:xs fw:600 c:primary tt:upper ls:wide">Baseline &mdash; 22 chars</span>
					<CodeBlock code={'<div layout="row center g4">'} />
				</div>
			</div>
		</div>
	</div>
</section>

<!-- Features -->
<section layout="container" class="py:16">
	<div layout="col g8">
		<div layout="col g3" class="ta:center">
			<h2 class="t:2xl fw:700 c:text">Why Baseline?</h2>
			<p class="t:base c:text-muted max-w:prose mx:auto lh:relaxed">
				Modern CSS is powerful enough. Your utility framework shouldn't need a build step, a config file, or a JIT compiler.
			</p>
		</div>

		<div layout="grid @md:cols-2 @lg:cols-3 g6">
			<div layout="col g2" class="p:6 bg:surface r:xl b:1 bc:border-subtle">
				<h3 class="t:base fw:600 c:text">Semantic Naming</h3>
				<p class="t:sm c:text-muted lh:relaxed">
					<code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">bg:primary</code> not
					<code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">bg-blue-600</code>.
					Colours mean something. Theming is one variable change.
				</p>
			</div>
			<div layout="col g2" class="p:6 bg:surface r:xl b:1 bc:border-subtle">
				<h3 class="t:base fw:600 c:text">Layout Attributes</h3>
				<p class="t:sm c:text-muted lh:relaxed">
					<code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">layout="row center g4"</code> reads like a design spec.
					Structure and style are separate concerns.
				</p>
			</div>
			<div layout="col g2" class="p:6 bg:surface r:xl b:1 bc:border-subtle">
				<h3 class="t:base fw:600 c:text">Zero Build Step</h3>
				<p class="t:sm c:text-muted lh:relaxed">
					One <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">&lt;link&gt;</code> tag.
					No PostCSS, no Vite plugin, no purging. Ship the whole framework at 10 KB gzipped.
				</p>
			</div>
			<div layout="col g2" class="p:6 bg:surface r:xl b:1 bc:border-subtle">
				<h3 class="t:base fw:600 c:text">Smart State Variants</h3>
				<p class="t:sm c:text-muted lh:relaxed">
					<code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">:hover>bg</code> reads the base colour's hover token automatically.
					One class works for every semantic colour.
				</p>
			</div>
			<div layout="col g2" class="p:6 bg:surface r:xl b:1 bc:border-subtle">
				<h3 class="t:base fw:600 c:text">CSP Compliant</h3>
				<p class="t:sm c:text-muted lh:relaxed">
					No inline styles, ever. Enterprise-ready out of the box.
					Strict Content Security Policy without <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">unsafe-inline</code>.
				</p>
			</div>
			<div layout="col g2" class="p:6 bg:surface r:xl b:1 bc:border-subtle">
				<h3 class="t:base fw:600 c:text">LLM Optimised</h3>
				<p class="t:sm c:text-muted lh:relaxed">
					Self-documenting names. 49% fewer tokens. Reference schema and recipes included for predictable AI code generation.
				</p>
			</div>
		</div>
	</div>
</section>

<!-- Dark mode teaser -->
<section class="bg:surface-sunken py:16 bt:1 bb:1 bc:border-subtle">
	<div layout="container">
		<div layout="col @md:row g8 center">
			<div layout="col g3" style="flex: 1;">
				<h2 class="t:2xl fw:700 c:text">Dark mode? One attribute.</h2>
				<p class="t:base c:text-muted lh:relaxed">
					No <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">dark:</code> prefixes scattered everywhere.
					Themes cascade through CSS custom properties. Stack accessibility themes too.
				</p>
				<CodeBlock code={'<html data-theme="dark">\n\n<!-- Composable -->\n<html data-theme="dark high-contrast large-text">'} />
			</div>
			<div layout="col g4" style="flex: 1;">
				<div data-theme="dark" class="p:6 bg:surface r:xl b:1 bc:border-subtle">
					<div layout="col g3">
						<h3 class="t:base fw:600 c:text">Dark theme preview</h3>
						<p class="t:sm c:text-muted lh:relaxed">Every component adapts automatically. No extra classes needed.</p>
						<div layout="row g2">
							<button class="px:4 py:2 bg:primary c:text-inverse r:md t:sm fw:500">Primary</button>
							<button class="px:4 py:2 bg:surface c:text r:md t:sm b:1 bc:border">Secondary</button>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</section>

<!-- CTA -->
<section layout="container" class="py:16">
	<div layout="col g4 center" class="ta:center">
		<h2 class="t:2xl fw:700 c:text">Ready to build?</h2>
		<p class="t:base c:text-muted">Read the docs, browse 20 production-ready recipes, or jump straight in.</p>
		<div layout="row g3 center wrap">
			<a href="{base}/docs/getting-started"
				class="px:5 py:3 bg:primary c:text-inverse r:lg fw:600 t:sm td:none tr:colors :hover>bg :focus>ring">
				Documentation
			</a>
			<a href="{base}/recipes"
				class="px:5 py:3 bg:surface c:text r:lg fw:600 t:sm td:none b:1 bc:border tr:colors :hover>bg:neutral-2">
				Browse Recipes
			</a>
		</div>
	</div>
</section>
