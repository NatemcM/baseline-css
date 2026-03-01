<script>
	import CodeBlock from '$lib/components/CodeBlock.svelte';
</script>

<svelte:head>
	<title>State Variants — Baseline CSS</title>
</svelte:head>

<div layout="col g8">
	<div layout="col g3">
		<h1 class="t:3xl fw:700 c:text">State Variants</h1>
		<p class="t:lg c:text-muted lh:relaxed">Generic and explicit state handling — hover, focus, active, disabled, group, peer, and has.</p>
	</div>

	<!-- Generic states -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Generic State Pattern</h2>
		<p class="t:sm c:text-muted lh:relaxed">
			Semantic <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">bg:*</code> utilities set private CSS variables for their hover, active, and ring colours.
			Generic state classes read these variables, so <strong class="c:text">one class works for every colour</strong>.
		</p>
		<CodeBlock code={`<!-- :hover>bg automatically uses danger-hover because bg:danger set it -->
<button class="bg:danger c:text-inverse r:md px:4 py:2
  tr:colors :hover>bg :active>bg :focus>ring">
  Delete
</button>`} />
		<p class="t:sm c:text-muted lh:relaxed">Adding a new colour to your design system automatically gets hover, active, and focus states.</p>

		<!-- Live demo -->
		<div layout="row wrap g3" class="p:4 bg:surface-sunken r:lg">
			{#each ['primary', 'secondary', 'accent', 'success', 'warning', 'danger', 'info'] as color}
				<button class="px:4 py:2 bg:{color} c:text-inverse r:md t:sm fw:500 tr:colors :hover>bg :active>bg :focus>ring">
					{color}
				</button>
			{/each}
		</div>
	</section>

	<!-- How it works -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">How It Works</h2>
		<p class="t:sm c:text-muted lh:relaxed">Each semantic <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">bg:*</code> utility sets private custom properties:</p>
		<CodeBlock code={`.bg\\:primary {
  background-color: var(--primary);
  --_bg-hover: var(--primary-hover);
  --_bg-active: var(--primary-active);
  --_ring: var(--primary);
}

/* One class covers ALL semantic colours */
.\\:hover\\>bg:hover { background-color: var(--_bg-hover); }
.\\:active\\>bg:active { background-color: var(--_bg-active); }
.\\:focus\\>ring:focus-visible {
  outline: var(--focus-ring-width) solid var(--_ring);
  outline-offset: var(--focus-ring-offset);
}`} lang="css" />

		<div class="overflow:auto">
			<table class="w:full t:sm">
				<thead>
					<tr class="bb:2 bc:border">
						<th class="ta:left py:2 px:3 c:text fw:600">Generic</th>
						<th class="ta:left py:2 px:3 c:text fw:600">Reads from</th>
						<th class="ta:left py:2 px:3 c:text fw:600">Set by</th>
					</tr>
				</thead>
				<tbody>
					{#each [
						[':hover>bg', '--_bg-hover', 'bg:primary, bg:danger, etc.'],
						[':active>bg', '--_bg-active', 'bg:primary, bg:danger, etc.'],
						[':focus>ring', '--_ring', 'bg:* (defaults to primary)'],
						[':hover>sh', '--_sh-hover', 'sh:xs, sh:sm, sh:md, sh:lg, sh:xl']
					] as [generic, reads, set]}
						<tr class="bb:1 bc:border-subtle">
							<td class="py:2 px:3 ff:mono t:xs c:primary">{generic}</td>
							<td class="py:2 px:3 ff:mono t:xs c:text-muted">{reads}</td>
							<td class="py:2 px:3 t:xs c:text-muted">{set}</td>
						</tr>
					{/each}
				</tbody>
			</table>
		</div>
	</section>

	<!-- Explicit -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Explicit Overrides</h2>
		<p class="t:sm c:text-muted lh:relaxed">For non-semantic colours or when you need a specific target:</p>
		<CodeBlock code={`<!-- Neutral bg doesn't have state vars, use explicit -->
<button class="bg:surface :hover>bg:neutral-2 :focus>ring:primary">
  Outline
</button>

<!-- Override the generic hover with a specific colour -->
<button class="bg:primary :hover>bg:danger">Custom Hover</button>`} />
	</section>

	<!-- Explicit variants table -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Explicit State Variants</h2>
		<div class="overflow:auto">
			<table class="w:full t:sm">
				<thead>
					<tr class="bb:2 bc:border">
						<th class="ta:left py:2 px:3 c:text fw:600">Prefix</th>
						<th class="ta:left py:2 px:3 c:text fw:600">Selector</th>
						<th class="ta:left py:2 px:3 c:text fw:600">Examples</th>
					</tr>
				</thead>
				<tbody>
					{#each [
						[':hover>', ':hover', ':hover>bg:neutral-2, :hover>c:text, :hover>o:90, :hover>scale:105'],
						[':focus>', ':focus-visible', ':focus>bc:text, :focus>bc:primary, :focus>ring'],
						[':active>', ':active', ':active>bg, :active>scale:98'],
						[':disabled>', ':disabled', ':disabled>o:50, :disabled>cursor:not-allowed'],
						[':focus-within>', ':focus-within', ':focus-within>bc:primary, :focus-within>ring'],
						['peer-*', 'peer ~ &', 'peer-checked:, peer-focus:, peer-invalid:'],
						['group-*', 'group:hover &', 'group-hover:, group-focus:'],
						['has-*', ':has(*)', 'has-checked:, has-invalid:, has-focus:']
					] as [prefix, selector, examples]}
						<tr class="bb:1 bc:border-subtle">
							<td class="py:2 px:3 ff:mono t:xs c:primary">{prefix}</td>
							<td class="py:2 px:3 ff:mono t:xs c:text-muted">{selector}</td>
							<td class="py:2 px:3 t:xs c:text-muted">{examples}</td>
						</tr>
					{/each}
				</tbody>
			</table>
		</div>
	</section>

	<!-- Group / Peer / Has -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Group, Peer & Has</h2>
		<p class="t:sm c:text-muted lh:relaxed">Advanced state targeting without JavaScript.</p>

		<h3 class="t:base fw:600 c:text">Group hover</h3>
		<p class="t:sm c:text-muted lh:relaxed">Style children when a parent is hovered:</p>
		<CodeBlock code={`<div class="group">
  <h3 class="group-hover:c:primary tr:colors">Title changes on hover</h3>
  <p class="group-hover:c:text tr:colors">So does this text</p>
</div>`} />

		<h3 class="t:base fw:600 c:text mt:4">Peer state</h3>
		<p class="t:sm c:text-muted lh:relaxed">Style siblings based on a peer's state:</p>
		<CodeBlock code={`<input type="checkbox" class="peer" />
<label class="peer-checked:c:primary peer-checked:fw:600">
  Styled when checked
</label>`} />

		<h3 class="t:base fw:600 c:text mt:4">Has selector</h3>
		<p class="t:sm c:text-muted lh:relaxed">Style parents based on descendant state using CSS <code class="ff:mono t:xs bg:surface-sunken px:1 r:sm">:has()</code>:</p>
		<CodeBlock code={`<!-- Border turns red when any input inside is invalid -->
<div class="has-invalid:bc:danger b:1 bc:border r:lg p:4">
  <input type="email" required />
</div>

<!-- Card highlights when its checkbox is checked -->
<div class="has-checked:bc:primary has-checked:bg:primary-subtle b:1 bc:border r:lg p:4">
  <input type="checkbox" />
  <span>Select this card</span>
</div>`} />
	</section>

	<!-- Structural -->
	<section layout="col g3">
		<h2 class="t:xl fw:600 c:text">Structural Variants</h2>
		<div class="overflow:auto">
			<table class="w:full t:sm">
				<thead>
					<tr class="bb:2 bc:border">
						<th class="ta:left py:2 px:3 c:text fw:600">Class</th>
						<th class="ta:left py:2 px:3 c:text fw:600">Selector</th>
					</tr>
				</thead>
				<tbody>
					{#each [
						['first:*', ':first-child'],
						['last:*', ':last-child'],
						['odd:*', ':nth-child(odd)'],
						['even:*', ':nth-child(even)'],
						['placeholder:*', '::placeholder']
					] as [cls, selector]}
						<tr class="bb:1 bc:border-subtle">
							<td class="py:2 px:3 ff:mono t:xs c:primary">{cls}</td>
							<td class="py:2 px:3 ff:mono t:xs c:text-muted">{selector}</td>
						</tr>
					{/each}
				</tbody>
			</table>
		</div>
	</section>
</div>
