<script>
	import Nav from '$lib/components/Nav.svelte';
	let { children } = $props();
</script>

<Nav />
<main>
	{@render children()}
</main>

<footer class="py:8 px:6 bt:1 bc:border-subtle mt:16">
	<div layout="container">
		<div layout="row center-between" class="@md:flex-row">
			<p class="t:sm c:text-muted">MIT License &mdash; Baseline CSS</p>
			<div layout="row g4" class="mt:4 @md:mt:0">
				<a href="https://github.com/NatemcM/baseline-css" class="t:sm c:text-muted td:none :hover>c:text">GitHub</a>
			</div>
		</div>
	</div>
</footer>

<style>
	:global(body) {
		margin: 0;
		min-height: 100dvh;
	}
	:global(*, *::before, *::after) {
		box-sizing: border-box;
	}
</style>
