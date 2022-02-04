<template>
	<p v-if="errorMessage" class="error-message">{{ errorMessage }}</p>

	<div v-if="!loading" class="pokemon-detail">
		<div class="pokemon-detail-header">
			<div>
				<h2 class="pokemon-detail-name">{{ this.pokemon.name }}</h2>
				<div class="pokemon-detail-type">
					<span
						v-for="(value, index) in this.pokemon.types"
						:key="index"
						:class="value.type.name"
					>
						{{ value.type.name }}
					</span>
				</div>
			</div>
			<span class="pokemon-detail-id">#{{ this.pokemon.id }}</span>
		</div>

		<div class="pokemon-detail-image">
			<img
				v-show="this.frontView"
				:src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${this.pokemon.id}.png`"
				alt="Pokemon Sprite Front"
			/>
			<img
				v-show="!this.frontView"
				:src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/back/${this.pokemon.id}.png`"
				alt="Pokemon Sprite Back"
			/>
		</div>

		<div class="pokemon-detail-body">
			<div class="pokemon-detail-description">
				<div class="physics">
					<div class="keys">
						<span>XP</span>
						<span>Height</span>
						<span>Weight</span>
					</div>
					<div class="values">
						<span>{{ this.pokemon.base_experience }}</span>
						<span>{{ this.pokemon.height / 10 }} m</span>
						<span>{{ this.pokemon.weight / 10 }} kg</span>
					</div>
				</div>

				<div class="abilities">
					<span class="abilities-title">Abilities</span>
					<div class="abilities-content">
						<span
							v-for="(value, index) in this.pokemon.abilities"
							:key="index"
						>
							{{ value.ability.name }}
						</span>
					</div>
				</div>
			</div>
			<div class="d-pad">
				<button @click="togglePokemonImage()">
					<i class="fas fa-caret-left"></i>
				</button>
				<button @click="togglePokemonImage()">
					<i class="fas fa-caret-right"></i>
				</button>
			</div>
		</div>
	</div>

	<div v-else class="loading-image">
		<img :src="loadingImage" />
	</div>
</template>

<script>
	export default {
		name: "Pokemon",
		data() {
			return {
				name: this.$route.params.name,
				pokemon: {},
				frontView: true,
				loading: true,
				loadingImage: require("../assets/loading.gif"),
				errorMessage: "",
			};
		},
		methods: {
			async fetchPokemon(name) {
				const res = await fetch(
					`https://pokeapi.co/api/v2/pokemon/${name}/`
				);

				if (res.status === 404) {
					this.errorMessage = "Pokemon not found, try again.";
					throw new Error(this.errorMessage);
				}

				if (!res.ok) {
					this.errorMessage = `Something went wrong with the server: ${res.status} ${res.statusText}. Try again later`;
					throw new Error(this.errorMessage);
				}
				const data = await res.json();
				return data;
			},
			togglePokemonImage() {
				this.frontView = !this.frontView;
			},
		},
		async created() {
			try {
				this.pokemon = await this.fetchPokemon(this.name);
			} catch (e) {
				console.error(e);
				return;
			}

			this.loading = false;
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
	.pokemon-detail {
		width: 100%;
		padding: 2rem;
		margin-top: 2rem;
		background-color: white;
		border-radius: 5px;
		border: solid 1px black;
		display: flex;
		flex-direction: column;
		box-shadow: 0 2px 2px rgba(0, 0, 0, 0.1), 0 5px 5px rgba(0, 0, 0, 0.1);
		overflow: hidden;
	}
	.pokemon-detail-header {
		width: 100%;
		display: flex;
		align-items: center;
		justify-content: space-between;
	}
	.pokemon-detail-name {
		font-size: 2rem;
		text-transform: capitalize;
	}
	.pokemon-detail-type {
		margin-top: 1rem;
	}
	.pokemon-detail-type span {
		color: white;
		margin-right: 1rem;
		border-radius: 5px;
		border: solid 1px black;
		padding: 0.5rem;
		display: inline-block;
		box-shadow: 0 2px 2px rgba(0, 0, 0, 0.1), 0 5px 5px rgba(0, 0, 0, 0.1);
		text-transform: capitalize;
	}
	.pokemon-detail-type .grass {
		background: rgb(3, 139, 44);
	}
	.pokemon-detail-type .poison {
		background: rgb(74, 7, 105);
	}
	.pokemon-detail-type .water {
		background: rgb(8, 135, 219);
	}
	.pokemon-detail-type .dragon {
		background: rgb(27, 2, 68);
	}
	.pokemon-detail-type .ice {
		background: rgb(78, 199, 255);
	}
	.pokemon-detail-type .flying {
		background: rgb(145, 215, 255);
	}
	.pokemon-detail-type .fire {
		background: rgb(238, 135, 17);
	}
	.pokemon-detail-type .ghost {
		background: rgb(74, 52, 87);
	}
	.pokemon-detail-type .fighting {
		background: rgb(122, 0, 0);
	}
	.pokemon-detail-type .normal {
		background: rgb(104, 104, 104);
	}
	.pokemon-detail-type .psychic {
		background: rgb(195, 0, 255);
	}
	.pokemon-detail-type .bug {
		background: rgb(52, 87, 6);
	}
	.pokemon-detail-type .dark {
		background: rgb(43, 43, 43);
	}
	.pokemon-detail-type .steel {
		background: rgb(116, 116, 116);
	}
	.pokemon-detail-type .fairy {
		background: rgb(248, 165, 237);
	}
	.pokemon-detail-type .electric {
		background: rgb(255, 217, 1);
	}
	.pokemon-detail-type .rock {
		background: rgb(88, 95, 100);
	}
	.pokemon-detail-type .ground {
		background: rgb(92, 70, 70);
	}
	.pokemon-detail-image {
		width: 100%;
		margin-top: 2rem;
		background-color: rgb(42, 42, 42);
		border: solid 1px black;
		border-radius: 5px;
		text-align: center;
		box-shadow: 0 2px 2px rgba(0, 0, 0, 0.1), 0 5px 5px rgba(0, 0, 0, 0.1);
	}
	.pokemon-detail-image img {
		width: 50%;
		height: 50%;
	}
	.pokemon-detail-body {
		width: 100%;
		margin-top: 1rem;
		display: flex;
		justify-content: space-between;
	}
	.pokemon-detail-description {
		display: flex;
		flex-direction: column;
		flex: 1;
	}
	.physics {
		display: flex;
		justify-content: space-between;
	}
	.physics div {
		display: flex;
		flex-direction: column;
	}
	.physics .keys span {
		color: rgb(98, 98, 98);
		margin-top: 1rem;
	}
	.physics .values {
		align-items: flex-end;
	}
	.physics .values span {
		margin-top: 1rem;
	}
	.abilities {
		display: flex;
		justify-content: space-between;
		margin-top: 1rem;
	}
	.abilities-title {
		color: rgb(98, 98, 98);
	}
	.abilities-content {
		display: flex;
		align-items: flex-end;
		flex-direction: column;
	}
	.abilities-content span {
		text-transform: capitalize;
	}
	.d-pad {
		display: flex;
		align-items: center;
		justify-content: center;
		flex: 1;
	}
	.d-pad button {
		padding: 0.2rem 1rem;
		background-color: black;
		color: white;
		border-radius: 5px;
		border: none;
		box-shadow: 0 0.2em rgb(107, 107, 107);
		cursor: pointer;
	}
	.d-pad button:active {
		box-shadow: none;
		position: relative;
		top: 0.2em;
	}
	.d-pad .fas {
		font-size: 1.5rem;
	}
</style>
