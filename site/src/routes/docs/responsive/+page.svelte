<script>
	import CodeBlock from '$lib/components/CodeBlock.svelte';
</script>

<svelte:head>
	<title>Responsive Design — Baseline CSS</title>
</svelte:head>

<div layout="col g8">
	<div layout="col g3">
		<h1 class="t:3xl fw:700 c:text">Responsive Design</h1>
		<p class="t:lg c:text-muted lh:relaxed">Mobile-first breakpoints using the <code class="ff:mono t:sm bg:surface-sunken px:1 r:sm">@</code> prefix, mirroring CSS at-rules.</p>
	</div>

	<!-- Breakpoints -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Breakpoints</h2>
		<div class="overflow:auto">
			<table class="w:full t:sm">
				<thead>
					<tr class="bb:2 bc:border">
						<th class="ta:left py:2 px:3 c:text fw:600">Prefix</th>
						<th class="ta:left py:2 px:3 c:text fw:600">Min Width</th>
						<th class="ta:left py:2 px:3 c:text fw:600">CSS</th>
					</tr>
				</thead>
				<tbody>
					{#each [
						['@sm:', '640px', '@media (width >= 40rem)'],
						['@md:', '768px', '@media (width >= 48rem)'],
						['@lg:', '1024px', '@media (width >= 64rem)'],
						['@xl:', '1280px', '@media (width >= 80rem)'],
						['@2xl:', '1536px', '@media (width >= 96rem)']
					] as [prefix, width, css]}
						<tr class="bb:1 bc:border-subtle">
							<td class="py:2 px:3 ff:mono t:xs c:primary fw:600">{prefix}</td>
							<td class="py:2 px:3 c:text">{width}</td>
							<td class="py:2 px:3 ff:mono t:xs c:text-muted">{css}</td>
						</tr>
					{/each}
				</tbody>
			</table>
		</div>
	</section>

	<!-- Usage -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Usage</h2>
		<p class="t:sm c:text-muted lh:relaxed">Works in both layout attributes and utility classes:</p>
		<CodeBlock code={`<!-- Stack on mobile, row on tablet -->
<div layout="col @md:row center g4 @md:g8">

  <!-- Smaller text on mobile, larger on desktop -->
  <h1 class="t:2xl @lg:t:4xl fw:700">Responsive Heading</h1>

  <!-- Adjust padding at breakpoints -->
  <div class="p:4 @md:p:6 @lg:p:8">
    Content
  </div>
</div>`} />
	</section>

	<!-- Available variants -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Available Responsive Variants</h2>
		<p class="t:sm c:text-muted lh:relaxed">Responsive variants are available for:</p>
		<div layout="grid @md:cols-2 g3">
			{#each [
				['Display', 'd:none, d:block, d:flex, d:grid'],
				['Spacing', 'p, px, py, mb, mt, mx'],
				['Typography', 't:sm, t:lg, t:xl, etc.'],
				['Text align', 'ta:left, ta:center, ta:right'],
				['Width', 'w:full, w:half, w:auto'],
				['Max width', 'max-w:sm through max-w:xl'],
				['Order', 'order:first, order:last, order:none'],
				['Layout', 'row, col, cols-*, gap, spans']
			] as [category, examples]}
				<div class="p:3 bg:surface-sunken r:md">
					<span class="t:sm fw:600 c:text">{category}</span>
					<p class="t:xs c:text-muted ff:mono mt:1">{examples}</p>
				</div>
			{/each}
		</div>
	</section>

	<!-- Common patterns -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Common Patterns</h2>

		<h3 class="t:base fw:600 c:text">Responsive grid</h3>
		<CodeBlock code={`<!-- 1 col on mobile → 2 cols on tablet → 3 cols on desktop -->
<div layout="grid cols-1 @md:cols-2 @lg:cols-3 g6">`} />

		<h3 class="t:base fw:600 c:text mt:4">Hide/show at breakpoints</h3>
		<CodeBlock code={`<!-- Hidden on mobile, visible on md+ -->
<div class="d:none @md:d:block">Desktop only</div>

<!-- Visible on mobile, hidden on md+ -->
<div class="d:block @md:d:none">Mobile only</div>`} />

		<h3 class="t:base fw:600 c:text mt:4">Responsive typography</h3>
		<CodeBlock code={`<h1 class="t:2xl @md:t:3xl @lg:t:5xl fw:700">
  Scales with viewport
</h1>`} />
	</section>

	<!-- Live demo -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Live Demo</h2>
		<p class="t:sm c:text-muted lh:relaxed">Resize your browser to see this grid respond:</p>
		<div class="p:4 bg:surface-sunken r:lg">
			<div layout="grid cols-1 @md:cols-2 @lg:cols-3 g4">
				{#each [1, 2, 3] as n}
					<div class="p:4 bg:surface r:lg b:1 bc:border-subtle ta:center">
						<span class="t:lg fw:600 c:text">Card {n}</span>
						<p class="t:sm c:text-muted mt:2">Responsive grid item</p>
					</div>
				{/each}
			</div>
		</div>
	</section>
</div>
