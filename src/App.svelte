<script>
	import Card from './Card.svelte';

</script>

<main>
	<h1>Svelte Memory Card game</h1>
	<Card title={"Madza"} image={"https://source.unsplash.com/random/300x200"}/>
</main>

<style>
	h1 {
		text-align: center;
	}

	main {
		max-width: 800px;
		margin: 0 auto;
	}
</style>