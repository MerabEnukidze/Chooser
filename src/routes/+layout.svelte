<script>
	import Header from '$lib/Header.svelte';
	import '../app.css';
	import Meta from "$lib/Meta.svelte";
	import Footer from '$lib/Footer.svelte';
	import { page } from '$app/stores';

	$: isMoods = $page.url.pathname === '/moods';
</script>

<div class="app" class:app-locked={isMoods}>
	<Meta />
	<Header />
	<main class="w-full">
		<slot />
	</main>
	<Footer />
</div>

<style>
	.app {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
	}

	.app-locked {
		height: 100vh;
		max-height: 100vh;
		overflow: hidden;
	}

	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		min-height: 0;
	}
</style>
