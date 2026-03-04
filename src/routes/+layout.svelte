<script lang="ts">
	import '../app.css';
	import Navigation from '$lib/components/Navigation.svelte';

	let { children } = $props();
</script>

<svelte:head>
	<title>País de Pandereta</title>
	<meta
		name="description"
		content="Plataforma abierta de datos y herramientas ciudadanas."
	/>
</svelte:head>

<div class="min-h-screen bg-white">
	<Navigation />
	<main class="mx-auto max-w-3xl px-4 py-8">
		{@render children?.()}
	</main>
</div>
