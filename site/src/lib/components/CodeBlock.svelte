<script>
	let { code = '', lang = 'html' } = $props();
	let copied = $state(false);

	async function copy() {
		await navigator.clipboard.writeText(code);
		copied = true;
		setTimeout(() => copied = false, 2000);
	}
</script>

<div class="pos:relative">
	<pre class="ff:mono t:sm bg:surface-sunken p:4 r:lg overflow:auto lh:relaxed"><code>{code}</code></pre>
	<button onclick={copy}
		class="pos:absolute t:xs px:2 py:1 bg:surface r:md b:1 bc:border-subtle c:text-muted tr:colors :hover>bg:neutral-2"
		style="top: 0.5rem; right: 0.5rem;">
		{copied ? 'Copied!' : 'Copy'}
	</button>
</div>

<style>
	pre {
		margin: 0;
		white-space: pre;
		tab-size: 2;
	}
</style>
