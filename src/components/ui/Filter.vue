<template>
	<form @submit="onSubmit" class="filter-elements">
		<input
			class="filter"
			type="text"
			v-model="pokemonName"
			placeholder="Search a pokemon"
			autocomplete="off"
		/>
		<button class="btn-filter" type="submit">
			<i class="fas fa-search"></i>
		</button>
	</form>
</template>

<script>
	export default {
		name: "Filter",
		data() {
			return {
				pokemonName: "",
			};
		},
		methods: {
			onSubmit(e) {
				e.preventDefault();
				// Remove all spaces
				const pokemonName = this.pokemonName.replace(/\s+/g, "");
				// Validate is not empty
				if (pokemonName === "") {
					return;
				}
				// Check if is just letters
				if (!/^[a-zA-Z]*$/g.test(pokemonName)) {
					alert(
						"Please enter a valid pokemon name. (Only alphabet letters allowed)"
					);
					this.pokemonName = "";
					return;
				}
				// Send
				this.$router.push({
					path: `/about/${pokemonName.toLowerCase()}`,
				});
				this.pokemonName = "";
			},
		},
	};
</script>

<style scoped>
	.filter-elements {
		width: 100%;
		display: flex;
		align-items: end;
		margin-top: 2rem;
	}
	.filter {
		font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
			Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
		font-size: 1rem;
		width: 100%;
		outline: none;
		border: solid 1px black;
		border-radius: 5px;
		padding: 1rem;
		box-shadow: 0 2px 2px rgba(0, 0, 0, 0.1), 0 5px 5px rgba(0, 0, 0, 0.1);
	}
	.filter:focus {
		background-color: rgb(251, 251, 180);
	}
	.btn-filter {
		padding: 1rem;
		background-color: rgb(255 203 7);
		border-radius: 5px;
		border: solid 1px black;
		box-shadow: 0 0.2em rgb(107, 107, 107);
		cursor: pointer;
	}
	.btn-filter:active {
		box-shadow: none;
		position: relative;
		top: 0.2em;
	}
	.btn-filter .fas {
		font-size: 1rem;
		color: rgb(73, 73, 73);
	}
</style>
