<script>
	import { goto } from '$app/navigation';
	import { base } from '$app/paths';
	import { onMount } from 'svelte';

	onMount(() => {
		goto(`${base}/docs/getting-started`, { replaceState: true });
	});
</script>

<div layout="col center" class="py:16 ta:center">
	<p class="c:text-muted">Redirecting to Getting Started...</p>
</div>
