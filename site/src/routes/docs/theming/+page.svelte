<script>
	import CodeBlock from '$lib/components/CodeBlock.svelte';
</script>

<svelte:head>
	<title>Theming — Baseline CSS</title>
</svelte:head>

<div layout="col g8">
	<div layout="col g3">
		<h1 class="t:3xl fw:700 c:text">Theming</h1>
		<p class="t:lg c:text-muted lh:relaxed">Design tokens, dark mode, scoped themes, and composable accessibility — all without a build step.</p>
	</div>

	<!-- Design tokens -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Design Tokens</h2>
		<p class="t:sm c:text-muted lh:relaxed">Everything flows from CSS custom properties. Override them to customise your design:</p>
		<CodeBlock code={`:root {
  --primary: oklch(0.55 0.22 280);
  --primary-hover: oklch(0.48 0.22 280);
  --font-sans: 'Inter', system-ui, sans-serif;
  --r-md: 0.5rem;
  --s-4: 1.125rem;
}`} lang="css" />
		<p class="t:sm c:text-muted lh:relaxed">No config files. No rebuild. Just CSS.</p>
	</section>

	<!-- Semantic colours -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Semantic Colour System</h2>
		<p class="t:sm c:text-muted lh:relaxed">Every semantic colour has a full family of state variants:</p>
		<CodeBlock code={`/* Brand — each has base, hover, active, subtle */
--primary       --primary-hover      --primary-active     --primary-subtle
--secondary     --secondary-hover    --secondary-active   --secondary-subtle
--accent        --accent-hover       --accent-active      --accent-subtle

/* Feedback — same pattern */
--success       --success-hover      --success-active     --success-subtle
--warning       --warning-hover      --warning-active     --warning-subtle
--danger        --danger-hover       --danger-active      --danger-subtle
--info          --info-hover         --info-active        --info-subtle

/* Surfaces */
--surface       --surface-raised     --surface-sunken     --surface-overlay

/* Text */
--text          --text-muted         --text-faint         --text-inverse

/* Borders */
--border        --border-subtle      --border-strong`} lang="css" />
	</section>

	<!-- Dark mode -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Dark Mode</h2>
		<p class="t:sm c:text-muted lh:relaxed">One attribute. Every component adapts. No <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">dark:</code> prefixes.</p>
		<CodeBlock code={'<html data-theme="dark">'} />
		<p class="t:sm c:text-muted lh:relaxed">Toggle with JavaScript:</p>
		<CodeBlock code={`const root = document.documentElement;
root.dataset.theme = root.dataset.theme === 'dark' ? 'light' : 'dark';`} lang="js" />
		<p class="t:sm c:text-muted lh:relaxed">
			Baseline also respects <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">prefers-color-scheme: dark</code> automatically when no <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">data-theme</code> is set.
		</p>

		<!-- Live preview -->
		<div layout="grid @md:cols-2 g4">
			<div data-theme="light" class="p:5 bg:surface r:xl b:1 bc:border-subtle">
				<div layout="col g3">
					<span class="t:xs fw:600 c:text-muted tt:upper ls:wide">Light</span>
					<p class="t:sm c:text">Text adapts automatically.</p>
					<button class="px:3 py:1.5 bg:primary c:text-inverse r:md t:sm fw:500">Button</button>
				</div>
			</div>
			<div data-theme="dark" class="p:5 bg:surface r:xl b:1 bc:border-subtle">
				<div layout="col g3">
					<span class="t:xs fw:600 c:text-muted tt:upper ls:wide">Dark</span>
					<p class="t:sm c:text">Text adapts automatically.</p>
					<button class="px:3 py:1.5 bg:primary c:text-inverse r:md t:sm fw:500">Button</button>
				</div>
			</div>
		</div>
	</section>

	<!-- Scoped themes -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Scoped Themes</h2>
		<p class="t:sm c:text-muted lh:relaxed">Themes cascade through CSS custom properties, so you can scope them to any element:</p>
		<CodeBlock code={`<body data-theme="light">
  <!-- Light-themed page -->

  <section data-theme="dark" class="bg:surface p:8 r:lg">
    <!-- This section is dark-themed -->
    <p class="c:text">This text adapts automatically.</p>
  </section>
</body>`} />
	</section>

	<!-- Composable accessibility -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Composable Accessibility Themes</h2>
		<p class="t:sm c:text-muted lh:relaxed">Themes stack via space-separated values. Each theme only touches the variables it cares about:</p>
		<CodeBlock code={'<html data-theme="dark high-contrast large-text reduce-motion">'} />
		<div class="overflow:auto">
			<table class="w:full t:sm">
				<thead>
					<tr class="bb:2 bc:border">
						<th class="ta:left py:2 px:3 c:text fw:600">Theme</th>
						<th class="ta:left py:2 px:3 c:text fw:600">Effect</th>
					</tr>
				</thead>
				<tbody>
					{#each [
						['dark', 'Dark colour scheme'],
						['high-contrast', 'Stronger contrast ratios, heavier borders, bolder focus rings'],
						['large-text', 'Scaled-up typography for low vision'],
						['reduce-motion', 'Pauses all animations via --anim-state token']
					] as [theme, effect]}
						<tr class="bb:1 bc:border-subtle">
							<td class="py:2 px:3 ff:mono t:xs c:primary">{theme}</td>
							<td class="py:2 px:3 c:text-muted">{effect}</td>
						</tr>
					{/each}
				</tbody>
			</table>
		</div>
	</section>

	<!-- Base size -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Base Size Scaling</h2>
		<p class="t:sm c:text-muted lh:relaxed">
			The <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">--base-size</code> token controls the root font-size.
			Since all values use rem, changing this one variable scales the entire framework.
		</p>
		<CodeBlock code={`:root {
  --base-size: 100%;   /* default: 1rem = 16px */
  --base-size: 112.5%; /* larger:  1rem = 18px */
  --base-size: 87.5%;  /* smaller: 1rem = 14px */
}`} lang="css" />
	</section>
</div>
