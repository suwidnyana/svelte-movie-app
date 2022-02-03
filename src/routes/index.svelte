<script context="module">
	export async function load({ fetch }) {
		const response = await fetch(
			`https://api.themoviedb.org/3/movie/popular?api_key=d39e771b293f3dc36a0c9cb185d615bc&language=en-US&page=1`
		);
		const data = await response.json();

		return {
			props: {
				popular: data.results
			}
		};
	}
</script>

<script>
	import PopularMovies from '../components/PopularMovies.svelte';
	export let popular;
</script>

<section>
	<PopularMovies {popular} />
</section>
