<script context="module">
	export async function load({ fetch, params }) {
		const response = await fetch(
			`https://api.themoviedb.org/3/movie/${params.id}?api_key=d39e771b293f3dc36a0c9cb185d615bc&language=en-US`
		);
		const movieDetail = await response.json();
		console.log(movieDetail);
		return {
			props: { movieDetail }
		};
	}
</script>

<script>
	export let movieDetail;
	console.log(movieDetail);
	import { fly } from 'svelte/transition';
</script>

<div class="movie-detail" in:fly={{ y: 50, duration: 500, delay: 500 }} out:fly={{ duration: 500 }}>
	<div class="img-container">
		<img
			src={`https://image.tmdb.org/t/p/original/${movieDetail.backdrop_path}`}
			alt={movieDetail.title}
			width="900px"
		/>
	</div>
	<div class="txt-container">
		<h1>{movieDetail.title}</h1>
		<p class="overview">{movieDetail.overview}</p>
		<p>
			<span>Release Date:</span>
			{movieDetail.release_date}<br />
			<span>Budget:</span> ${movieDetail.budget}<br />
			<span>Rating:</span>
			{movieDetail.vote_average}<br />
			<span>Runtime:</span>
			{movieDetail.runtime} mins
		</p>
	</div>
</div>

<style>
	h1 {
		padding: 1rem 0rem 2rem;
	}
	p {
		padding: 1rem 0rem;
	}
	.img-container img {
		border-radius: 2%;
		margin: auto;
	}
	.movie-detail {
		margin: 2rem 20%;
	}
	span {
		font-weight: bold;
	}
</style>
