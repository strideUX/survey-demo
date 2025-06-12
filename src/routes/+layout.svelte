<script lang="ts">
	import '../app.css';

	let { children } = $props();
</script>

<main style="min-height: 100vh; width: 100vw;">
	{@render children()}
</main>

<style>
</style>
