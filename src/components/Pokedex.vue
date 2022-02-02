<template>
	<span v-if="errorMessage" class="error-message"> {{ errorMessage }}</span>

	<main v-if="!loading" class="list">
		<!-- Pokemon cardboxes -->
		<article v-for="(pokemon, index) in pokemons" :key="index">
			<img
				:src="
					imageUrl +
					pokemon.url
						.split('/')
						.filter((part) => {
							return part;
						})
						.pop() +
					'.png'
				"
				width="96"
				height="96"
				alt="Pokemon sprite"
			/>
			<span>{{ pokemon.name }}</span>
		</article>
		<!-- End cardbox -->
	</main>

	<main v-else class="loading-image">
		<img :src="loadingImage" alt="Loading gif" />
	</main>
</template>

<script>
	export default {
		name: "Pokedex",
		data() {
			return {
				pokemons: [],
				imageUrl:
					"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/",
				loading: true,
				loadingImage: require("../assets/loading.gif"),
				errorMessage: "",
			};
		},
		methods: {
			async fetchPokemons() {
				const res = await fetch(
					"https://pokeapi.co/api/v2/pokemon/?limit=5"
				);
				if (!res.ok) {
					this.errorMessage =
						"Something went wrong with the server. Try again later";
					this.loading = false;
					return;
				}
				const data = await res.json();
				return data.results;
			},
		},
		async created() {
			this.pokemons = await this.fetchPokemons();
			this.pokemons.length === 0 &&
				(this.errorMessage = "There are no pokemons to show.");
			this.loading = false;
		},
	};
</script>

<style scoped>
	.error-message {
		display: block;
		margin-top: 2rem;
		color: white;
	}
	.loading-image {
		display: flex;
		justify-content: center;
		margin-top: 4rem;
	}
	.loading-image img {
		max-width: 100%;
		height: 100px;
	}
	.list {
		margin-top: 2rem;
		display: flex;
		justify-content: space-around;
		flex-wrap: wrap;
	}
	article {
		width: 150px;
		height: 150px;
		background-color: white;
		border: solid 1px rgb(248, 248, 248);
		border-radius: 5px;
		padding: 1rem;
		cursor: pointer;
		margin-bottom: 1.5rem;
		text-transform: capitalize;
		text-align: center;
		box-shadow: 0 2px 2px rgba(0, 0, 0, 0.1), 0 5px 5px rgba(0, 0, 0, 0.1);
	}
	article:hover {
		background-color: lightyellow;
	}
</style>
