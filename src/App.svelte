<script>
	let query = '';
	let links = []
	const fetchQuery = async () => {
		const res = await fetch(`http://127.0.0.1:5001/search/${query}`)
		const json = await res.json()
		console.log(json)
		const unsorted = Object.entries(json)
		const sorted = unsorted.sort((a, b) => b[1] - a[1])
		links = sorted.map(([url, count]) => url)
		console.log(links)
	}
	const  onSubmit = () => {
		fetchQuery()
	}
</script>

<main>
	<form on:submit|preventDefault={onSubmit}>
		<input placeholder="enter search query" bind:value={query}>
	</form>
	<ul>
	{#each links as link}
		<li><a target="_blank" href={link}>
			{link}
		</a></li>
	{/each}
</ul>
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
