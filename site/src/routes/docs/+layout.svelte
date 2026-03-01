<script>
	import DocSidebar from '$lib/components/DocSidebar.svelte';
	let { children } = $props();
</script>

<div layout="container" class="py:8">
	<div layout="row g8">
		<DocSidebar />
		<article class="min-w:0" style="flex: 1;">
			{@render children()}
		</article>
	</div>
</div>
