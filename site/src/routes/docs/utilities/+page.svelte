<script>
	import CodeBlock from '$lib/components/CodeBlock.svelte';
</script>

<svelte:head>
	<title>Utilities Reference — Baseline CSS</title>
</svelte:head>

<div layout="col g8">
	<div layout="col g3">
		<h1 class="t:3xl fw:700 c:text">Utilities Reference</h1>
		<p class="t:lg c:text-muted lh:relaxed">Every utility class organised by domain. All follow the <code class="ff:mono t:sm bg:surface-sunken px:1 r:sm">domain:value</code> pattern.</p>
	</div>

	<!-- Spacing -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Spacing</h2>
		<p class="t:sm c:text-muted lh:relaxed">Padding and margin with directional prefixes.</p>
		<div class="overflow:auto">
			<table class="w:full t:sm">
				<thead>
					<tr class="bb:2 bc:border">
						<th class="ta:left py:2 px:3 c:text fw:600">Prefix</th>
						<th class="ta:left py:2 px:3 c:text fw:600">Direction</th>
					</tr>
				</thead>
				<tbody>
					{#each [
						['p / m', 'All sides'],
						['px / mx', 'Inline (left + right)'],
						['py / my', 'Block (top + bottom)'],
						['pt / mt', 'Top'],
						['pb / mb', 'Bottom'],
						['ps / ms', 'Inline start'],
						['pe / me', 'Inline end']
					] as [prefix, dir]}
						<tr class="bb:1 bc:border-subtle">
							<td class="py:2 px:3 ff:mono t:xs c:primary">{prefix}</td>
							<td class="py:2 px:3 c:text-muted">{dir}</td>
						</tr>
					{/each}
				</tbody>
			</table>
		</div>
		<p class="t:sm c:text-muted">
			<strong class="c:text">Values:</strong>
			<code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">0</code>
			<code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">0.5</code>
			<code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">1</code>
			<code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">1.5</code>
			<code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">2</code>
			<code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">3</code>
			<code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">4</code>
			<code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">5</code>
			<code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">6</code>
			<code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">8</code>
			<code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">10</code>
			<code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">12</code>
			<code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">16</code>
		</p>
		<p class="t:sm c:text-muted">
			Margin also supports: <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">mx:auto</code>
		</p>
	</section>

	<!-- Colours -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Colours</h2>

		<h3 class="t:base fw:600 c:text">Background — <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">bg:</code></h3>
		<p class="t:sm c:text-muted lh:relaxed ff:mono">
			primary · primary-subtle · secondary · secondary-subtle · accent · accent-subtle · success · success-subtle · warning · warning-subtle · danger · danger-subtle · info · info-subtle · surface · surface-raised · surface-sunken · surface-overlay · text · neutral-1 through neutral-9 · transparent
		</p>

		<h3 class="t:base fw:600 c:text mt:4">Text colour — <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">c:</code></h3>
		<p class="t:sm c:text-muted lh:relaxed ff:mono">
			text · text-muted · text-faint · text-inverse · surface · primary · secondary · accent · success · warning · danger · info · neutral-1 through neutral-9 · inherit
		</p>

		<h3 class="t:base fw:600 c:text mt:4">Border colour — <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">bc:</code></h3>
		<p class="t:sm c:text-muted lh:relaxed ff:mono">
			border · border-subtle · border-strong · text · primary · secondary · accent · success · warning · danger · info · transparent
		</p>
	</section>

	<!-- Typography -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Typography</h2>

		<h3 class="t:base fw:600 c:text">Font size — <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">t:</code></h3>
		<div layout="col g2">
			{#each [
				['t:xs', '0.75rem'],
				['t:sm', '0.875rem'],
				['t:base', '1rem'],
				['t:lg', '1.125rem'],
				['t:xl', '1.25rem'],
				['t:2xl', '1.5rem'],
				['t:3xl', '1.875rem'],
				['t:4xl', '2.25rem'],
				['t:5xl', '3rem']
			] as [cls, size]}
				<div layout="row center-start g4" class="py:1">
					<code class="ff:mono t:xs c:primary" style="min-width: 4rem;">{cls}</code>
					<span class="{cls} c:text">The quick brown fox</span>
					<span class="t:xs c:text-faint">{size}</span>
				</div>
			{/each}
		</div>

		<h3 class="t:base fw:600 c:text mt:4">Font weight — <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">fw:</code></h3>
		<p class="t:sm c:text-muted ff:mono">100 · 200 · 300 · 400 · 500 · 600 · 700 · 800 · 900</p>

		<h3 class="t:base fw:600 c:text mt:4">Font family — <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">ff:</code></h3>
		<p class="t:sm c:text-muted ff:mono">sans · serif · mono</p>

		<h3 class="t:base fw:600 c:text mt:4">Line height — <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">lh:</code></h3>
		<p class="t:sm c:text-muted ff:mono">tight · snug · base · relaxed · loose</p>

		<h3 class="t:base fw:600 c:text mt:4">Letter spacing — <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">ls:</code></h3>
		<p class="t:sm c:text-muted ff:mono">tight · normal · wide · wider</p>

		<h3 class="t:base fw:600 c:text mt:4">Text align — <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">ta:</code></h3>
		<p class="t:sm c:text-muted ff:mono">left · center · right · justify</p>

		<h3 class="t:base fw:600 c:text mt:4">Text decoration — <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">td:</code></h3>
		<p class="t:sm c:text-muted ff:mono">none · underline · line-through</p>

		<h3 class="t:base fw:600 c:text mt:4">Text transform — <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">tt:</code></h3>
		<p class="t:sm c:text-muted ff:mono">upper · lower · cap</p>

		<h3 class="t:base fw:600 c:text mt:4">Utilities</h3>
		<p class="t:sm c:text-muted ff:mono">truncate · line-clamp-2 · line-clamp-3</p>
	</section>

	<!-- Borders -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Borders</h2>

		<h3 class="t:base fw:600 c:text">Border width — <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">b:</code></h3>
		<p class="t:sm c:text-muted ff:mono">b:0 · b:1 · b:2 · bt:1 · bt:2 · bb:1 · bb:2 · bs:1 · bs:2 · be:1 · be:2</p>

		<h3 class="t:base fw:600 c:text mt:4">Border radius — <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">r:</code></h3>
		<div layout="row wrap g3" class="mt:2">
			{#each ['none', 'sm', 'md', 'lg', 'xl', '2xl', '3xl', 'full'] as val}
				<div layout="col center g1">
					<div class="bg:primary-subtle b:1 bc:primary r:{val}" style="width: 3rem; height: 3rem;"></div>
					<span class="t:xs c:text-muted ff:mono">r:{val}</span>
				</div>
			{/each}
		</div>
	</section>

	<!-- Shadows -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Shadows — <code class="ff:mono t:sm bg:surface-sunken px:1 r:sm">sh:</code></h2>
		<div layout="row wrap g4" class="mt:2">
			{#each ['none', 'xs', 'sm', 'md', 'lg', 'xl'] as val}
				<div layout="col center g1">
					<div class="bg:surface r:lg sh:{val}" style="width: 4rem; height: 4rem;"></div>
					<span class="t:xs c:text-muted ff:mono">sh:{val}</span>
				</div>
			{/each}
		</div>
		<p class="t:sm c:text-muted lh:relaxed mt:2">
			Each shadow sets <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">--_sh-hover</code> to the next level, so <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">:hover>sh</code> auto-elevates.
		</p>
	</section>

	<!-- Sizing -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Sizing</h2>

		<h3 class="t:base fw:600 c:text">Width — <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">w:</code></h3>
		<p class="t:sm c:text-muted ff:mono">full · auto · screen · min · max · fit · half</p>

		<h3 class="t:base fw:600 c:text mt:4">Max width — <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">max-w:</code></h3>
		<p class="t:sm c:text-muted ff:mono">sm · md · lg · xl · full · prose</p>

		<h3 class="t:base fw:600 c:text mt:4">Height — <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">h:</code></h3>
		<p class="t:sm c:text-muted ff:mono">full · auto · screen · min · fit</p>

		<h3 class="t:base fw:600 c:text mt:4">Fixed size — <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">size:</code></h3>
		<p class="t:sm c:text-muted ff:mono">4 · 5 · 6 · 8 · 10 · 12 · 16</p>
	</section>

	<!-- Effects -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Effects</h2>

		<h3 class="t:base fw:600 c:text">Opacity — <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">o:</code></h3>
		<p class="t:sm c:text-muted ff:mono">0 · 5 · 10 · 20 · 25 · 30 · 40 · 50 · 60 · 70 · 75 · 80 · 90 · 100</p>

		<h3 class="t:base fw:600 c:text mt:4">Transitions — <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">tr:</code></h3>
		<p class="t:sm c:text-muted ff:mono">none · all · colors · shadow · opacity · transform</p>

		<h3 class="t:base fw:600 c:text mt:4">Duration — <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">dur:</code></h3>
		<p class="t:sm c:text-muted ff:mono">fast · base · slow · slower</p>

		<h3 class="t:base fw:600 c:text mt:4">Scale — <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">scale:</code></h3>
		<p class="t:sm c:text-muted ff:mono">95 · 98 · 100 · 102 · 105 · 110</p>

		<h3 class="t:base fw:600 c:text mt:4">Animations — <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">anim:</code></h3>
		<p class="t:sm c:text-muted ff:mono">spin · pulse · bounce · fade-in · slide-up · shake</p>
	</section>
</div>
