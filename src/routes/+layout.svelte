<script lang="ts">
	import favicon from '$lib/assets/favicon.svg';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<header>
<h1>Agropédia</h1>
	<nav>
		<a href="/">Home</a>
		<a href="/sobre">Sobre</a>
	</nav>
</header>



{@render children()}
