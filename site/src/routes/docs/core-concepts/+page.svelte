<script>
	import CodeBlock from '$lib/components/CodeBlock.svelte';
</script>

<svelte:head>
	<title>Core Concepts — Baseline CSS</title>
</svelte:head>

<div layout="col g8">
	<div layout="col g3">
		<h1 class="t:3xl fw:700 c:text">Core Concepts</h1>
		<p class="t:lg c:text-muted lh:relaxed">The principles behind Baseline CSS and how everything fits together.</p>
	</div>

	<!-- Two-layer styling -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Two-Layer Styling</h2>
		<p class="t:sm c:text-muted lh:relaxed">
			Baseline separates <strong class="c:text">structure</strong> from <strong class="c:text">style</strong>.
			The <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">layout</code> attribute tells you what an element does spatially.
			Classes tell you what it looks like.
		</p>
		<CodeBlock code={`<nav layout="row center-between g4"
     class="px:6 py:3 bg:surface bb:1 bc:border-subtle">
  <h1 class="t:sm fw:600 c:text">Logo</h1>
  <button class="px:4 py:2 bg:primary c:text-inverse r:md
    fw:500 t:sm tr:colors :hover>bg :focus>ring">
    Sign Up
  </button>
</nav>`} />
		<p class="t:sm c:text-muted lh:relaxed">
			No more decoding <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">flex items-center justify-between</code> to understand layout intent.
		</p>
	</section>

	<!-- Domain:value syntax -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Domain:Value Syntax</h2>
		<p class="t:sm c:text-muted lh:relaxed">
			Every utility class follows the <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">domain:value</code> pattern.
			The domain tells you <em>what</em> property, the value tells you <em>how</em>.
		</p>
		<div class="overflow:auto">
			<table class="w:full t:sm">
				<thead>
					<tr class="bb:2 bc:border">
						<th class="ta:left py:2 px:3 c:text fw:600">Domain</th>
						<th class="ta:left py:2 px:3 c:text fw:600">Property</th>
						<th class="ta:left py:2 px:3 c:text fw:600">Example</th>
					</tr>
				</thead>
				<tbody>
					{#each [
						['p', 'padding', 'p:4, px:6, py:2'],
						['m', 'margin', 'm:4, mx:auto, mt:6'],
						['bg', 'background-color', 'bg:primary, bg:surface'],
						['c', 'color', 'c:text, c:text-muted'],
						['t', 'font-size', 't:sm, t:xl, t:3xl'],
						['fw', 'font-weight', 'fw:400, fw:600, fw:700'],
						['r', 'border-radius', 'r:sm, r:md, r:lg, r:full'],
						['sh', 'box-shadow', 'sh:sm, sh:md, sh:lg'],
						['b', 'border', 'b:1, bt:1, bb:1'],
						['bc', 'border-color', 'bc:border, bc:primary'],
						['o', 'opacity', 'o:0, o:50, o:100'],
						['tr', 'transition', 'tr:all, tr:colors, tr:shadow'],
						['w / h', 'width / height', 'w:full, h:screen'],
						['z', 'z-index', 'z:dropdown, z:modal']
					] as [domain, prop, example]}
						<tr class="bb:1 bc:border-subtle">
							<td class="py:2 px:3 ff:mono t:xs c:primary">{domain}</td>
							<td class="py:2 px:3 c:text-muted">{prop}</td>
							<td class="py:2 px:3 ff:mono t:xs c:text">{example}</td>
						</tr>
					{/each}
				</tbody>
			</table>
		</div>
	</section>

	<!-- CSS layers -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">CSS Layers</h2>
		<p class="t:sm c:text-muted lh:relaxed">
			Baseline uses <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">@layer</code> to manage cascade priority.
			This means your custom CSS always wins over framework utilities &mdash; no <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">!important</code> needed.
		</p>
		<div layout="col g2">
			{#each [
				['1. Tokens', 'CSS custom properties for spacing, colours, typography'],
				['2. Reset', 'Minimal opinionated baseline styles'],
				['3. Theme', 'Composable themes via data-theme attribute'],
				['4. Layout', 'Structural composition via layout attribute'],
				['5. Utilities', 'Visual utility classes (domain:value)'],
				['6. Responsive', 'Breakpoint variants (@sm, @md, @lg, @xl, @2xl)'],
				['7. States', 'State variants (:hover>, :focus>, group-, peer-, has-)']
			] as [name, desc]}
				<div layout="row g3 center-start" class="p:3 bg:surface-sunken r:md">
					<span class="ff:mono t:xs c:primary fw:600" style="min-width: 6rem;">{name}</span>
					<span class="t:sm c:text-muted">{desc}</span>
				</div>
			{/each}
		</div>
	</section>

	<!-- Semantic colours -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Semantic Colours</h2>
		<p class="t:sm c:text-muted lh:relaxed">
			Baseline uses semantic colour tokens instead of arbitrary palettes. Changing your brand colour updates every button, link, and accent across your entire site.
		</p>
		<div layout="row wrap g3">
			{#each ['primary', 'secondary', 'accent', 'success', 'warning', 'danger', 'info'] as color}
				<div layout="col center g1">
					<div class="r:lg b:1 bc:border-subtle bg:{color}" style="width: 3.5rem; height: 3.5rem;"></div>
					<span class="t:xs c:text-muted ff:mono">{color}</span>
				</div>
			{/each}
		</div>
		<p class="t:sm c:text-muted lh:relaxed">
			Each colour has a full family: <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">base</code>, <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">hover</code>, <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">active</code>, and <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">subtle</code> variants.
		</p>
	</section>
</div>
