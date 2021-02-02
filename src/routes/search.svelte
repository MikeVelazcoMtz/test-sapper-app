<svelte:head>
	<title>Search page -Sapper App</title>

</svelte:head>

<script context="module">
	const API_KEY = "29ed1d64cc3508c30f08131eb1860d99";
	const BASE_URL = 'https://api.themoviedb.org/3';
	const API_SETTINGS = `?api_key=${API_KEY}&language=en-US`;

	export async function preload() {
		const URL = `${BASE_URL}/discover/movie${API_SETTINGS}&sort_by=popularity.desc`;
		const movies = await this.fetch(URL).then((res) => res.json()).then((data) => data.results);

		console.log(movies);

		return { movies };
	}
</script>

<script>
	import Item from '../components/Item.svelte';
	export let movies;
	const name= "user";
</script>

<main class="container">
	<div class="row">
		<div class="col-12 col-md-6 col-lg-8">
			<h1>Popular movies</h1>
			<div class="row">
				{#each movies as movie (movie.id)}
					<div class="col-4">
						<Item {movie} />
					</div>
				{:else}
					Loading...
				{/each}
			</div>
		</div>
		<div class="col-12 col-md-6 col-lg-4">
			<h1>Favorite Movies</h1>
		</div>
	</div>
</main>

