<script>
	import CodeBlock from '$lib/components/CodeBlock.svelte';
</script>

<svelte:head>
	<title>Benchmarks — Baseline CSS</title>
</svelte:head>

<div layout="container" class="py:8">
	<div layout="col g8">
		<div layout="col g3">
			<h1 class="t:3xl fw:700 c:text">Benchmarks</h1>
			<p class="t:lg c:text-muted lh:relaxed">How Baseline CSS compares to Tailwind CSS in file size, token count, and architecture.</p>
		</div>

		<!-- File size -->
		<section layout="col g3">
			<h2 class="t:xl fw:600 c:text">File Size</h2>
			<div class="overflow:auto">
				<table class="w:full t:sm">
					<thead>
						<tr class="bb:2 bc:border">
							<th class="ta:left py:2 px:3 c:text fw:600">Metric</th>
							<th class="ta:left py:2 px:3 c:primary fw:600">Baseline CSS</th>
							<th class="ta:left py:2 px:3 c:text-muted fw:600">Tailwind (full)</th>
							<th class="ta:left py:2 px:3 c:text-muted fw:600">Tailwind (purged)</th>
						</tr>
					</thead>
					<tbody>
						{#each [
							['Gzipped', '10 KB', '190 KB', '~3-10 KB'],
							['Brotli', '8 KB', '46 KB', '~2-5 KB'],
							['Uncompressed', '146 KB', '2,413 KB', '~10-50 KB'],
							['CSS Rules', '~620', 'Varies', 'Varies'],
							['Build step', 'None', 'Required', 'Required']
						] as [metric, baseline, full, purged]}
							<tr class="bb:1 bc:border-subtle">
								<td class="py:2 px:3 c:text fw:500">{metric}</td>
								<td class="py:2 px:3 c:primary fw:600">{baseline}</td>
								<td class="py:2 px:3 c:text-muted">{full}</td>
								<td class="py:2 px:3 c:text-muted">{purged}</td>
							</tr>
						{/each}
					</tbody>
				</table>
			</div>
			<p class="t:sm c:text-muted lh:relaxed">
				Baseline ships the <strong class="c:text">entire framework</strong> at 10 KB gzipped &mdash; comparable to a purged Tailwind build, but with zero build tooling.
			</p>
		</section>

		<!-- Token count -->
		<section layout="col g3">
			<h2 class="t:xl fw:600 c:text">HTML Token Count</h2>
			<p class="t:sm c:text-muted lh:relaxed">Characters in class/layout attributes. Lower is better &mdash; fewer tokens means faster LLM generation, smaller HTML, and easier reading.</p>

			<div layout="col g4">
				{#each [
					['Primary Button', 84, 185, '55%'],
					['Card', 33, 64, '48%'],
					['Form Input', 108, 193, '44%'],
					['Alert', 39, 75, '48%'],
					['Badge', 46, 77, '40%'],
					['Flex Row', 22, 55, '60%']
				] as [component, baseline, tailwind, savings]}
					<div layout="col g2">
						<div layout="row center-between">
							<span class="t:sm fw:600 c:text">{component}</span>
							<span class="t:sm fw:700 c:primary">{savings} fewer</span>
						</div>
						<div layout="col g1">
							<div layout="row center-start g2">
								<span class="t:xs c:primary fw:600" style="min-width: 4.5rem;">Baseline</span>
								<div class="h:6 bg:primary r:sm" style="width: {(baseline / tailwind) * 100}%;"></div>
								<span class="t:xs c:text-muted">{baseline}</span>
							</div>
							<div layout="row center-start g2">
								<span class="t:xs c:text-muted" style="min-width: 4.5rem;">Tailwind</span>
								<div class="h:6 bg:neutral-3 r:sm" style="width: 100%;"></div>
								<span class="t:xs c:text-muted">{tailwind}</span>
							</div>
						</div>
					</div>
				{/each}
			</div>

			<div class="p:5 bg:primary-subtle r:xl ta:center mt:4">
				<span class="t:3xl fw:700 c:primary">~49%</span>
				<p class="t:sm c:primary fw:500 mt:1">average token savings across components</p>
			</div>
		</section>

		<!-- Side by side -->
		<section layout="col g3">
			<h2 class="t:xl fw:600 c:text">Side-by-Side Comparison</h2>

			<h3 class="t:base fw:600 c:text">Primary Button</h3>
			<div layout="grid @md:cols-2 g4">
				<div layout="col g1">
					<span class="t:xs fw:600 c:primary tt:upper ls:wide">Baseline — 84 chars</span>
					<CodeBlock code={`<button class="px:4 py:2 bg:primary
  c:text-inverse r:md fw:500 t:sm
  tr:colors :hover>bg :focus>ring">
  Submit
</button>`} />
				</div>
				<div layout="col g1">
					<span class="t:xs fw:600 c:text-muted tt:upper ls:wide">Tailwind — 185 chars</span>
					<CodeBlock code={`<button class="px-4 py-2 bg-primary
  text-primary-foreground rounded-md
  font-medium text-sm transition-colors
  hover:bg-primary/90
  focus-visible:outline-none
  focus-visible:ring-2
  focus-visible:ring-ring">
  Submit
</button>`} />
				</div>
			</div>

			<h3 class="t:base fw:600 c:text mt:6">Layout</h3>
			<div layout="grid @md:cols-2 g4">
				<div layout="col g1">
					<span class="t:xs fw:600 c:primary tt:upper ls:wide">Baseline — 22 chars</span>
					<CodeBlock code={`<div layout="row center g4">`} />
				</div>
				<div layout="col g1">
					<span class="t:xs fw:600 c:text-muted tt:upper ls:wide">Tailwind — 55 chars</span>
					<CodeBlock code={`<div class="flex flex-row items-center
  justify-center gap-4">`} />
				</div>
			</div>

			<h3 class="t:base fw:600 c:text mt:6">Form Input</h3>
			<div layout="grid @md:cols-2 g4">
				<div layout="col g1">
					<span class="t:xs fw:600 c:primary tt:upper ls:wide">Baseline — 108 chars</span>
					<CodeBlock code={`<input class="px:3 py:2 bg:surface
  r:md b:1 bc:border t:sm c:text
  w:full outline:none tr:colors
  :focus>bc:text :focus>ring" />`} />
				</div>
				<div layout="col g1">
					<span class="t:xs fw:600 c:text-muted tt:upper ls:wide">Tailwind — 193 chars</span>
					<CodeBlock code={`<input class="px-3 py-2 bg-background
  rounded-md border border-input
  text-sm text-foreground w-full
  outline-none transition-colors
  focus-visible:border-foreground
  focus-visible:ring-2
  focus-visible:ring-ring" />`} />
				</div>
			</div>
		</section>

		<!-- Architecture comparison -->
		<section layout="col g3">
			<h2 class="t:xl fw:600 c:text">Architecture Comparison</h2>
			<div class="overflow:auto">
				<table class="w:full t:sm">
					<thead>
						<tr class="bb:2 bc:border">
							<th class="ta:left py:2 px:3 c:text fw:600">Feature</th>
							<th class="ta:left py:2 px:3 c:primary fw:600">Baseline CSS</th>
							<th class="ta:left py:2 px:3 c:text-muted fw:600">Tailwind CSS</th>
						</tr>
					</thead>
					<tbody>
						{#each [
							['Build step', 'None', 'Required (PostCSS/Vite)'],
							['CSP compliant', 'Yes (zero inline styles)', 'Partial (arbitrary values)'],
							['Layout system', 'layout attribute', 'Utility classes'],
							['Theming', 'data-theme composable', 'CSS variables + config'],
							['Dark mode', 'Composable theme', 'dark: variant'],
							['State hover', ':hover>bg (generic)', 'hover:bg-* (per-class)'],
							['Accessibility', 'Built-in themes', 'Manual'],
							['Scoped themes', 'Any element', 'Manual'],
							['Full framework size', '10 KB gzipped', '190 KB gzipped']
						] as [feature, baseline, tailwind]}
							<tr class="bb:1 bc:border-subtle">
								<td class="py:2 px:3 c:text fw:500">{feature}</td>
								<td class="py:2 px:3 c:primary">{baseline}</td>
								<td class="py:2 px:3 c:text-muted">{tailwind}</td>
							</tr>
						{/each}
					</tbody>
				</table>
			</div>
		</section>

		<!-- Why it matters -->
		<section layout="col g3">
			<h2 class="t:xl fw:600 c:text">Why Fewer Tokens Matter</h2>
			<div layout="grid @md:cols-2 g4">
				{#each [
					['LLM Cost', 'AI tools generate HTML by tokens. ~49% fewer class tokens means ~49% less generation cost and latency.'],
					['Readability', 'Shorter classes are easier to scan. bg:primary vs bg-primary text-primary-foreground.'],
					['No Build Step', 'Baseline ships as a single CSS file. No PostCSS, no purging, no config.'],
					['CSP Compliance', 'Zero inline styles required. Enterprise-ready Content Security Policy.']
				] as [title, desc]}
					<div class="p:4 bg:surface-sunken r:lg">
						<h3 class="t:sm fw:600 c:text">{title}</h3>
						<p class="t:xs c:text-muted lh:relaxed mt:1">{desc}</p>
					</div>
				{/each}
			</div>
		</section>
	</div>
</div>
