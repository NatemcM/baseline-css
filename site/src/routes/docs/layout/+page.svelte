<script>
	import CodeBlock from '$lib/components/CodeBlock.svelte';
</script>

<svelte:head>
	<title>Layout System — Baseline CSS</title>
</svelte:head>

<div layout="col g8">
	<div layout="col g3">
		<h1 class="t:3xl fw:700 c:text">Layout System</h1>
		<p class="t:lg c:text-muted lh:relaxed">
			The <code class="ff:mono t:sm bg:surface-sunken px:1 r:sm">layout</code> attribute handles all structural composition &mdash; direction, alignment, grid, and gap.
		</p>
	</div>

	<!-- Basics -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Basic Usage</h2>
		<CodeBlock code={`<!-- Flex row, vertically centred, space-between, gap of 1rem -->
<div layout="row center-between g4">

<!-- Grid, 3 columns, gap of 1.5rem -->
<div layout="grid cols-3 g6">

<!-- Column stack, items stretched, gap of 0.5rem -->
<div layout="col stretch g2">

<!-- Centred container with max-width -->
<div layout="container">`} />
	</section>

	<!-- Direction -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Direction</h2>
		<div class="overflow:auto">
			<table class="w:full t:sm">
				<thead>
					<tr class="bb:2 bc:border">
						<th class="ta:left py:2 px:3 c:text fw:600">Token</th>
						<th class="ta:left py:2 px:3 c:text fw:600">Effect</th>
					</tr>
				</thead>
				<tbody>
					{#each [
						['row', 'flex-direction: row (horizontal)'],
						['col', 'flex-direction: column (vertical)'],
						['grid', 'display: grid'],
						['inline', 'display: inline-flex'],
						['hidden', 'display: none']
					] as [token, effect]}
						<tr class="bb:1 bc:border-subtle">
							<td class="py:2 px:3 ff:mono t:xs c:primary">{token}</td>
							<td class="py:2 px:3 c:text-muted">{effect}</td>
						</tr>
					{/each}
				</tbody>
			</table>
		</div>
	</section>

	<!-- Alignment -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Alignment Tokens</h2>
		<p class="t:sm c:text-muted lh:relaxed">
			Combine <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">align-items</code> and <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">justify-content</code> into a single readable token.
		</p>
		<div class="overflow:auto">
			<table class="w:full t:sm">
				<thead>
					<tr class="bb:2 bc:border">
						<th class="ta:left py:2 px:3 c:text fw:600">Token</th>
						<th class="ta:left py:2 px:3 c:text fw:600">align-items</th>
						<th class="ta:left py:2 px:3 c:text fw:600">justify-content</th>
					</tr>
				</thead>
				<tbody>
					{#each [
						['center', 'center', 'center'],
						['center-between', 'center', 'space-between'],
						['center-start', 'center', 'flex-start'],
						['center-end', 'center', 'flex-end'],
						['center-around', 'center', 'space-around'],
						['center-evenly', 'center', 'space-evenly'],
						['start', 'flex-start', 'flex-start'],
						['start-between', 'flex-start', 'space-between'],
						['end', 'flex-end', 'flex-end'],
						['stretch', 'stretch', '—'],
						['baseline', 'baseline', '—']
					] as [token, align, justify]}
						<tr class="bb:1 bc:border-subtle">
							<td class="py:2 px:3 ff:mono t:xs c:primary">{token}</td>
							<td class="py:2 px:3 ff:mono t:xs c:text-muted">{align}</td>
							<td class="py:2 px:3 ff:mono t:xs c:text-muted">{justify}</td>
						</tr>
					{/each}
				</tbody>
			</table>
		</div>
	</section>

	<!-- Gap -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Gap</h2>
		<p class="t:sm c:text-muted lh:relaxed">Gap tokens use the spacing scale:</p>
		<CodeBlock code={'g0  g0.5  g1  g1.5  g2  g3  g4  g5  g6  g8  g10  g12  g16'} />
	</section>

	<!-- Grid -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Grid</h2>
		<CodeBlock code={`<!-- 3-column grid -->
<div layout="grid cols-3 g4">
  <div>1</div>
  <div>2</div>
  <div>3</div>
</div>

<!-- Responsive grid: 1 col → 2 cols → 3 cols -->
<div layout="grid cols-1 @md:cols-2 @lg:cols-3 g6">

<!-- Spanning columns -->
<div layout="span-2">  <!-- spans 2 columns -->
<div layout="span-full"> <!-- spans all columns -->`} />

		<!-- Live grid demo -->
		<div class="p:4 bg:surface-sunken r:lg">
			<div layout="grid cols-3 g3">
				{#each [1, 2, 3, 4, 5, 6] as n}
					<div class="p:4 bg:primary-subtle c:primary ta:center r:md t:sm fw:600">{n}</div>
				{/each}
			</div>
		</div>
	</section>

	<!-- Flex child tokens -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Flex Child Tokens</h2>
		<div class="overflow:auto">
			<table class="w:full t:sm">
				<thead>
					<tr class="bb:2 bc:border">
						<th class="ta:left py:2 px:3 c:text fw:600">Token</th>
						<th class="ta:left py:2 px:3 c:text fw:600">Effect</th>
					</tr>
				</thead>
				<tbody>
					{#each [
						['fill', 'flex: 1 1 0% (fill available space)'],
						['grow', 'flex-grow: 1'],
						['shrink-0', 'flex-shrink: 0'],
						['self-start', 'align-self: flex-start'],
						['self-center', 'align-self: center'],
						['self-end', 'align-self: flex-end'],
						['self-stretch', 'align-self: stretch'],
						['wrap', 'flex-wrap: wrap'],
						['nowrap', 'flex-wrap: nowrap']
					] as [token, effect]}
						<tr class="bb:1 bc:border-subtle">
							<td class="py:2 px:3 ff:mono t:xs c:primary">{token}</td>
							<td class="py:2 px:3 c:text-muted">{effect}</td>
						</tr>
					{/each}
				</tbody>
			</table>
		</div>
	</section>

	<!-- Container -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Container</h2>
		<CodeBlock code={`<div layout="container">     <!-- max-width: 80rem, centred -->
<div layout="container-sm">  <!-- max-width: 40rem -->
<div layout="container-md">  <!-- max-width: 48rem -->
<div layout="container-lg">  <!-- max-width: 64rem -->`} />
	</section>
</div>
