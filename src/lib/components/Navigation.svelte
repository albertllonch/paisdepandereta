<script lang="ts">
	import { page } from '$app/state';

	let mobileMenuOpen = $state(false);

	const navigation = [
		{ name: 'Inicio', href: '/', icon: '🏠' },
		{
			name: 'Herramientas',
			href: '/herramientas',
			icon: '🔧',
			submenu: [
				{ name: 'Comparadores de Gasto', href: '/herramientas/comparadores', icon: '📊' },
				{ name: 'Generador de Formularios', href: '/herramientas/formularios', icon: '📝' },
				{ name: 'Reportar Trámites', href: '/herramientas/reportar', icon: '⚠️' }
			]
		},
		{ name: 'Blog', href: '/blog', icon: '📰' },
		{ name: 'Datos Abiertos', href: '/datos', icon: '📈' },
		{ name: 'Comunidad', href: '/comunidad', icon: '👥' },
		{ name: 'Acerca de', href: '/acerca-de', icon: 'ℹ️' }
	];

	function toggleMobileMenu() {
		mobileMenuOpen = !mobileMenuOpen;
	}

	function closeMobileMenu() {
		mobileMenuOpen = false;
	}
</script>

<nav class="border-b-4 border-yellow-400 bg-white shadow-lg">
	<div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
		<div class="flex h-16 justify-between">
			<!-- Logo and brand -->
			<div class="flex items-center">
				<a href="/" class="flex items-center space-x-2">
					<span class="text-2xl">🇪🇸</span>
					<div class="flex flex-col">
						<span class="text-lg leading-none font-bold text-red-600">País de</span>
						<span class="text-lg leading-none font-bold text-yellow-600">Pandereta</span>
					</div>
				</a>
			</div>

			<!-- Desktop Navigation -->
			<div class="hidden items-center space-x-8 md:flex">
				{#each navigation as item (item.href)}
					<div class="group relative">
						<a
							href={item.href}
							data-sveltekit-preload-data="hover"
							class="flex items-center space-x-1 rounded-md px-3 py-2 text-sm font-medium transition-colors duration-200
								   {page.url.pathname === item.href
								? 'bg-red-50 text-red-600'
								: 'text-gray-700 hover:bg-red-50 hover:text-red-600'}"
						>
							<span class="text-base">{item.icon}</span>
							<span>{item.name}</span>
						</a>

						<!-- Submenu dropdown -->
						{#if item.submenu}
							<div
								class="ring-opacity-5 invisible absolute left-0 z-50 mt-2 w-56 rounded-md bg-white opacity-0 shadow-lg ring-1 ring-black transition-all duration-200 group-hover:visible group-hover:opacity-100"
							>
								<div class="py-1">
									{#each item.submenu as subitem (subitem.href)}
										<a
											href={subitem.href}
											data-sveltekit-preload-data="hover"
											class="flex items-center space-x-2 px-4 py-2 text-sm text-gray-700 transition-colors duration-200 hover:bg-red-50 hover:text-red-600"
										>
											<span>{subitem.icon}</span>
											<span>{subitem.name}</span>
										</a>
									{/each}
								</div>
							</div>
						{/if}
					</div>
				{/each}
			</div>

			<!-- Mobile menu button -->
			<div class="flex items-center md:hidden">
				<button
					onclick={toggleMobileMenu}
					class="inline-flex items-center justify-center rounded-md p-2 text-gray-700 hover:bg-red-50 hover:text-red-600 focus:ring-2 focus:ring-red-500 focus:outline-none focus:ring-inset"
					aria-expanded="false"
				>
					<span class="sr-only">Abrir menú principal</span>
					{#if !mobileMenuOpen}
						<svg class="block h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M4 6h16M4 12h16M4 18h16"
							/>
						</svg>
					{:else}
						<svg class="block h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M6 18L18 6M6 6l12 12"
							/>
						</svg>
					{/if}
				</button>
			</div>
		</div>
	</div>

	<!-- Mobile Navigation -->
	{#if mobileMenuOpen}
		<div class="md:hidden">
			<div class="space-y-1 border-t border-gray-200 bg-gray-50 px-2 pt-2 pb-3 sm:px-3">
				{#each navigation as item (item.href)}
					<div>
						<a
							href={item.href}
							data-sveltekit-preload-data="hover"
							onclick={closeMobileMenu}
							class="flex items-center space-x-2 rounded-md px-3 py-2 text-base font-medium transition-colors duration-200
								   {page.url.pathname === item.href
								? 'bg-red-100 text-red-600'
								: 'text-gray-700 hover:bg-red-50 hover:text-red-600'}"
						>
							<span class="text-lg">{item.icon}</span>
							<span>{item.name}</span>
						</a>

						<!-- Mobile submenu -->
						{#if item.submenu}
							<div class="ml-6 space-y-1">
								{#each item.submenu as subitem (subitem.href)}
									<a
										href={subitem.href}
										data-sveltekit-preload-data="hover"
										onclick={closeMobileMenu}
										class="flex items-center space-x-2 rounded-md px-3 py-2 text-sm text-gray-600 transition-colors duration-200 hover:bg-red-50 hover:text-red-600"
									>
										<span>{subitem.icon}</span>
										<span>{subitem.name}</span>
									</a>
								{/each}
							</div>
						{/if}
					</div>
				{/each}
			</div>
		</div>
	{/if}
</nav>
