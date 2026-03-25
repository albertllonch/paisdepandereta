<script module lang="ts">
	export interface NavItem {
		name: string;
		href: string;
		visible?: boolean;
	}
</script>

<script lang="ts">
	import { page } from '$app/state';

	const defaultNavItems: NavItem[] = [
		{ name: 'Inicio', href: '/' },
		{ name: 'Blog', href: '/blog', visible: false },
		{ name: 'Acerca de', href: '/acerca-de' }
	];

	let { navItems = defaultNavItems }: { navItems?: NavItem[] } = $props();
	let items = $derived(navItems ?? defaultNavItems);
</script>

<nav class="border-b border-gray-200 bg-white">
	<div class="mx-auto max-w-4xl px-4">
		<div class="flex h-12 items-center justify-between">
			<a href="/" class="text-sm font-medium text-gray-900 hover:text-gray-600">
				País de Pandereta
			</a>

			<div class="flex items-center gap-6">
				{#each items.filter((item) => item.visible !== false) as item (item.href)}
					<a
						href={item.href}
						data-sveltekit-preload-data="hover"
						class="text-sm transition-colors {page.url.pathname === item.href
							? 'font-medium text-gray-900'
							: 'text-gray-500 hover:text-gray-900'}"
					>
						{item.name}
					</a>
				{/each}
			</div>
		</div>
	</div>
</nav>
