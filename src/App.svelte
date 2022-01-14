<script>
	//https://www.youtube.com/watch?v=QdStKZkNWm4
	import Plyr from 'plyr';
	export let name;
	const player = new Plyr('#player');

</script>

<main>
	<h1>Hello {name}!</h1>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>

	<div class="container">
		<div id="player" data-plyr-provider="youtube" data-plyr-embed-id="QdStKZkNWm4"></div>
	</div>
	<!-- Plyr resources and browser polyfills are specified in the pen settings -->
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>