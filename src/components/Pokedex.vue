<template>
	<span v-if="errorMessage" class="error-message">
		{{ serverErrorMsg }}
	</span>

	<main v-if="!loading" class="list">
		<!-- Pokemon cardboxes -->
		<article
			v-for="(pokemon, index) in pokemons"
			:key="index"
			@click="$router.push({ path: `/about/${pokemon.name}` })"
		>
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

	<div class="pagination-buttons">
		<button @click="loadPrev()" v-if="showPrevButton" class="btn">
			<i class="fas fa-caret-left"></i>
		</button>
		<button @click="loadNext()" v-if="showNextButton" class="btn">
			<i class="fas fa-caret-right"></i>
		</button>
	</div>
</template>

<script>
	export default {
		name: "Pokedex",
		props: {
			language: {
				type: String,
				default: "en",
			},
		},
		/*eslint-disable */
		computed: {
			serverErrorMsg() {
				if (this.language === "en") {
					return "Something went wrong with the server, please try again later.";
				}
				if (this.language === "es") {
					return "Ha ocurrido un error en el servidor, por favor intentalo más tarde.";
				}
			},
		},
		/*eslint-enable */
		data() {
			return {
				pokemons: [],
				url: "https://pokeapi.co/api/v2/pokemon/?limit=5",
				imageUrl:
					"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/",
				loading: true,
				loadingImage: require("../assets/loading.gif"),
				showPrevButton: false,
				showNextButton: false,
				nextUrl: "",
				prevUrl: "",
				errorMessage: "",
			};
		},
		methods: {
			async fetchPokemons() {
				const res = await fetch(this.url);
				if (!res.ok) {
					this.errorMessage = `Something went wrong with the server: ${res.status}`;
					throw new Error(this.errorMessage);
				}
				const data = await res.json();
				this.showPrevButton = false;
				this.showNextButton = false;
				if (data.next) {
					this.showNextButton = true;
					this.nextUrl = data.next;
				}
				if (data.previous) {
					this.showPrevButton = true;
					this.prevUrl = data.previous;
				}
				this.pokemons = data.results;
				this.loading = false;
			},
			loadNext() {
				this.url = this.nextUrl;
				this.fetchPokemons();
			},
			loadPrev() {
				this.url = this.prevUrl;
				this.fetchPokemons();
			},
		},
		created() {
			try {
				this.fetchPokemons();
			} catch (e) {
				console.error(e);
				return;
			}
		},
	};
</script>

<style scoped>
	.error-message {
		display: block;
		margin-top: 2rem;
		color: black;
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
		height: 160px;
		background-color: white;
		border: solid 1px black;
		border-radius: 5px;
		padding: 1rem;
		cursor: pointer;
		margin-bottom: 1.5rem;
		text-transform: capitalize;
		text-align: center;
		box-shadow: 0 2px 2px rgba(0, 0, 0, 0.1), 0 5px 5px rgba(0, 0, 0, 0.1);
		overflow: hidden;
	}
	article:hover {
		background-color: rgb(251, 251, 180);
	}
	.pagination-buttons {
		display: flex;
		justify-content: space-around;
		margin-top: 2rem;
	}
	.pagination-buttons .btn {
		padding: 0.2rem 1rem;
		background-color: black;
		color: white;
		border-radius: 5px;
		border: none;
		box-shadow: 0 0.2em rgb(107, 107, 107);
		cursor: pointer;
	}
	.pagination-buttons .btn:active {
		box-shadow: none;
		position: relative;
		top: 0.2em;
	}
	.fas {
		font-size: 1.5rem;
	}
</style>
