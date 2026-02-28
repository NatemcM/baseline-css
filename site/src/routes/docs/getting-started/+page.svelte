<script>
	import CodeBlock from '$lib/components/CodeBlock.svelte';
</script>

<svelte:head>
	<title>Getting Started — Baseline CSS</title>
</svelte:head>

<div layout="col g8">
	<div layout="col g3">
		<h1 class="t:3xl fw:700 c:text">Getting Started</h1>
		<p class="t:lg c:text-muted lh:relaxed">Add Baseline CSS to your project in under 30 seconds. No build tools required.</p>
	</div>

	<!-- CDN -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">CDN</h2>
		<p class="t:sm c:text-muted lh:relaxed">The fastest way to start. Drop this into your HTML <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">&lt;head&gt;</code>:</p>
		<CodeBlock code={'<link rel="stylesheet" href="https://unpkg.com/baseline-css@latest/baseline.css">'} />
	</section>

	<!-- npm -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">npm</h2>
		<CodeBlock code={'npm install baseline-css'} lang="bash" />
		<p class="t:sm c:text-muted lh:relaxed">Then import it in your entry file:</p>
		<CodeBlock code={"import 'baseline-css/baseline.css';"} lang="js" />
	</section>

	<!-- Download -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Download</h2>
		<p class="t:sm c:text-muted lh:relaxed">
			Grab <a href="https://github.com/NatemcM/baseline-css" class="c:primary td:underline">baseline.css</a> from GitHub, drop it in your project, and link it:
		</p>
		<CodeBlock code={'<link rel="stylesheet" href="/css/baseline.css">'} />
	</section>

	<!-- First component -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Your First Component</h2>
		<p class="t:sm c:text-muted lh:relaxed">Here's a card with a button. Notice how <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">layout</code> handles structure and classes handle appearance:</p>
		<CodeBlock code={`<div layout="col g4" class="p:6 bg:surface r:xl b:1 bc:border sh:md">
  <h3 class="t:lg fw:600 c:text">Welcome</h3>
  <p class="t:sm c:text-muted lh:relaxed">
    You're using Baseline CSS. No build step needed.
  </p>
  <button class="px:4 py:2 bg:primary c:text-inverse r:md
    fw:500 t:sm tr:colors :hover>bg :focus>ring">
    Get Started
  </button>
</div>`} />

		<!-- Live preview -->
		<div class="p:6 bg:surface-sunken r:xl b:1 bc:border-subtle">
			<div layout="col g4" class="p:6 bg:surface r:xl b:1 bc:border sh:md max-w:sm">
				<h3 class="t:lg fw:600 c:text">Welcome</h3>
				<p class="t:sm c:text-muted lh:relaxed">You're using Baseline CSS. No build step needed.</p>
				<button class="px:4 py:2 bg:primary c:text-inverse r:md fw:500 t:sm tr:colors :hover>bg :focus>ring">
					Get Started
				</button>
			</div>
		</div>
	</section>

	<!-- What's included -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">What's Included</h2>
		<p class="t:sm c:text-muted lh:relaxed">The single <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">baseline.css</code> file gives you everything:</p>
		<div layout="grid @md:cols-2 g4">
			<div layout="col g1" class="p:4 bg:surface-sunken r:lg">
				<span class="t:sm fw:600 c:text">1,758 utility classes</span>
				<span class="t:xs c:text-muted">Spacing, colours, typography, borders, shadows, animations, and more</span>
			</div>
			<div layout="col g1" class="p:4 bg:surface-sunken r:lg">
				<span class="t:sm fw:600 c:text">25 state variant types</span>
				<span class="t:xs c:text-muted">Hover, focus, active, disabled, group, peer, has, and structural</span>
			</div>
			<div layout="col g1" class="p:4 bg:surface-sunken r:lg">
				<span class="t:sm fw:600 c:text">5 responsive breakpoints</span>
				<span class="t:xs c:text-muted">sm, md, lg, xl, 2xl with mobile-first approach</span>
			</div>
			<div layout="col g1" class="p:4 bg:surface-sunken r:lg">
				<span class="t:sm fw:600 c:text">Composable themes</span>
				<span class="t:xs c:text-muted">Dark mode, high contrast, large text, reduce motion &mdash; stackable</span>
			</div>
		</div>
	</section>
</div>
