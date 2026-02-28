<script>
	import { base } from '$app/paths';
	import { page } from '$app/state';

	const sections = [
		{ title: 'Getting Started', href: `${base}/docs/getting-started` },
		{ title: 'Core Concepts', href: `${base}/docs/core-concepts` },
		{ title: 'Layout', href: `${base}/docs/layout` },
		{ title: 'Utilities', href: `${base}/docs/utilities` },
		{ title: 'Theming', href: `${base}/docs/theming` },
		{ title: 'Responsive', href: `${base}/docs/responsive` },
		{ title: 'States', href: `${base}/docs/states` }
	];
</script>

<aside class="d:none @lg:d:block" style="min-width: 14rem;">
	<nav layout="col g1" class="pos:sticky" style="top: 4rem;">
		<span class="t:xs fw:600 c:text-muted tt:upper ls:wide mb:2">Documentation</span>
		{#each sections as s}
			<a href={s.href}
				class="t:sm td:none py:1 px:3 r:md tr:colors"
				class:bg:primary-subtle={page.url.pathname === s.href}
				class:c:text={page.url.pathname === s.href}
				class:fw:600={page.url.pathname === s.href}
				class:c:text-muted={page.url.pathname !== s.href}>
				{s.title}
			</a>
		{/each}
	</nav>
</aside>
