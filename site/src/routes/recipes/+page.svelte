<script>
	import CodeBlock from '$lib/components/CodeBlock.svelte';
	import recipes from '$lib/data/recipes.json';

	let expandedId = $state(null);

	function toggleExpand(id) {
		expandedId = expandedId === id ? null : id;
	}

	function formatHtml(html) {
		// Basic formatting: add newlines after > for readability
		return html
			.replace(/></g, '>\n<')
			.replace(/\n\n+/g, '\n')
			.substring(0, 800) + (html.length > 800 ? '\n...' : '');
	}
</script>

<svelte:head>
	<title>Recipes — Baseline CSS</title>
</svelte:head>

<div layout="container" class="py:8">
	<div layout="col g8">
		<div layout="col g3">
			<h1 class="t:3xl fw:700 c:text">Recipes</h1>
			<p class="t:lg c:text-muted lh:relaxed">
				20 production-ready UI components. Each recipe is complete, copy-pasteable HTML using only Baseline CSS classes.
			</p>
		</div>

		<!-- Recipe cards -->
		<div layout="grid @md:cols-2 g6">
			{#each recipes.recipes as recipe}
				<div layout="col g3" class="p:5 bg:surface r:xl b:1 bc:border-subtle">
					<div layout="row center-between">
						<span class="px:2 py:0.5 bg:primary-subtle c:primary t:xs fw:600 r:full">#{recipe.id}</span>
					</div>
					<h3 class="t:lg fw:600 c:text">{recipe.name}</h3>
					<p class="t:sm c:text-muted lh:relaxed">{recipe.description}</p>
					<div layout="row wrap g1">
						{#each recipe.tags.slice(0, 4) as tag}
							<span class="px:2 py:0.5 bg:surface-sunken c:text-muted t:xs r:md ff:mono">{tag}</span>
						{/each}
					</div>
					<button
						onclick={() => toggleExpand(recipe.id)}
						class="px:4 py:2 bg:surface c:text r:md t:sm fw:500 b:1 bc:border-subtle tr:colors :hover>bg:neutral-2 w:full">
						{expandedId === recipe.id ? 'Hide Code' : 'View Code'}
					</button>
					{#if expandedId === recipe.id}
						<div class="mt:2">
							<CodeBlock code={formatHtml(recipe.html)} lang="html" />
						</div>
					{/if}
				</div>
			{/each}
		</div>

		<!-- LLM usage -->
		<section layout="col g3" class="p:6 bg:surface-sunken r:xl b:1 bc:border-subtle">
			<h2 class="t:xl fw:600 c:text">Using with LLMs</h2>
			<p class="t:sm c:text-muted lh:relaxed">
				Feed <code class="ff:mono t:xs bg:surface px:1 r:sm">baseline-recipes.json</code> alongside
				<code class="ff:mono t:xs bg:surface px:1 r:sm">baseline-reference.json</code> to any LLM for accurate Baseline CSS code generation.
			</p>
			<CodeBlock code={`// Example prompt:
"Using the Baseline CSS framework (reference and recipes attached),
build me a settings page with a sidebar navigation and form sections."`} />
		</section>
	</div>
</div>
