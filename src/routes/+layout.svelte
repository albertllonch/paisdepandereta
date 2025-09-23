<script lang="ts">
	import '../app.css';
	import favicon from '$lib/assets/favicon.svg';
	import Navigation from '$lib/components/Navigation.svelte';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
	<title>País de Pandereta - Plataforma de Transparencia y Herramientas Ciudadanas</title>
	<meta
		name="description"
		content="Plataforma abierta que ofrece herramientas digitales y datos contrastados para facilitar la relación con la burocracia en España."
	/>
</svelte:head>

<div class="min-h-screen bg-gray-50">
	<Navigation />
	<main class="container mx-auto px-4 py-8">
		{@render children?.()}
	</main>
</div>
