<script>
	import { base } from '$app/paths';
	import { page } from '$app/state';

	let theme = $state('light');

	function toggleTheme() {
		theme = theme === 'light' ? 'dark' : 'light';
		document.documentElement.dataset.theme = theme;
	}

	let mobileOpen = $state(false);
</script>

<nav layout="row center-between sticky" class="px:6 py:3 bg:surface bb:1 bc:border-subtle z:sticky">
	<div layout="row center g6">
		<a href="{base}/" class="t:lg fw:700 c:text td:none ls:tight">
			Baseline<span class="c:text-muted fw:400">.css</span>
		</a>
		<div layout="row center g4" class="d:none @md:d:flex">
			<a href="{base}/docs/getting-started" class="c:text-muted t:sm td:none tr:colors :hover>c:text"
				class:c:text={page.url.pathname.startsWith(`${base}/docs`)}>Docs</a>
			<a href="{base}/recipes" class="c:text-muted t:sm td:none tr:colors :hover>c:text"
				class:c:text={page.url.pathname.startsWith(`${base}/recipes`)}>Recipes</a>
			<a href="{base}/benchmarks" class="c:text-muted t:sm td:none tr:colors :hover>c:text"
				class:c:text={page.url.pathname.startsWith(`${base}/benchmarks`)}>Benchmarks</a>
		</div>
	</div>

	<div layout="row center g3">
		<a href="https://github.com/NatemcM/baseline-css" class="c:text-muted t:sm td:none :hover>c:text d:none @md:d:inline">GitHub</a>
		<button onclick={toggleTheme}
			class="px:3 py:1 t:sm bg:surface c:text r:md tr:colors :hover>bg:neutral-2 b:1 bc:border-subtle">
			{theme === 'light' ? 'Dark' : 'Light'}
		</button>
		<button onclick={() => mobileOpen = !mobileOpen}
			class="px:2 py:1 t:sm bg:surface c:text r:md b:1 bc:border-subtle d:block @md:d:none">
			Menu
		</button>
	</div>
</nav>

{#if mobileOpen}
	<div layout="col g2" class="px:6 py:4 bg:surface bb:1 bc:border-subtle d:block @md:d:none">
		<a href="{base}/docs/getting-started" class="c:text t:sm td:none py:1" onclick={() => mobileOpen = false}>Docs</a>
		<a href="{base}/recipes" class="c:text t:sm td:none py:1" onclick={() => mobileOpen = false}>Recipes</a>
		<a href="{base}/benchmarks" class="c:text t:sm td:none py:1" onclick={() => mobileOpen = false}>Benchmarks</a>
		<a href="https://github.com/NatemcM/baseline-css" class="c:text-muted t:sm td:none py:1">GitHub</a>
	</div>
{/if}
