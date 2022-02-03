<template>
	<div class="pokemon-detail">
		<div class="pokemon-detail-header">
			<div>
				<h2 class="pokemon-detail-name">Bulbausur</h2>
				<div class="pokemon-detail-type">
					<span>Fire</span>
					<span>Flying</span>
				</div>
			</div>
			<span class="pokemon-detail-id">003</span>
		</div>

		<div class="pokemon-detail-image">
			<img
				src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/1.png"
				alt="Pokemon Sprite"
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
						<span>225</span>
						<span>1.7m</span>
						<span>250kg</span>
					</div>
				</div>

				<div class="abilities">
					<span class="abilities-title">Abilities</span>
					<div class="abilities-content">
						<span>Grow</span>
						<span>Attack</span>
					</div>
				</div>
			</div>
			<div class="d-pad">
				<button><i class="fas fa-caret-left"></i></button>
				<button><i class="fas fa-caret-right"></i></button>
			</div>
		</div>
	</div>
</template>

<script>
	export default {
		name: "Pokemon",
	};
</script>

<style scoped>
	.pokemon-detail {
		width: 100%;
		padding: 2rem;
		margin-top: 2rem;
		background-color: white;
		border-radius: 5px;
		border: solid 1px rgb(248, 248, 248);
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
	.pokemon-detail-type {
		margin-top: 1rem;
	}
	.pokemon-detail-type span {
		color: rgb(98, 98, 98);
		margin-right: 1rem;
		border: 1px solid rgb(98, 98, 98);
		border-radius: 5px;
		padding: 0.5rem;
	}
	.pokemon-detail-image {
		width: 100%;
		margin-top: 2rem;
		background-color: rgb(42, 42, 42);
		border-radius: 5px;
		text-align: center;
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
