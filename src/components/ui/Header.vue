<template>
	<header>
		<router-link to="/">
			<img class="logo" alt="Pokedex logo" src="../../assets/logo.svg" />
		</router-link>
	</header>
</template>

<script>
	export default {
		name: "Header",
	};
</script>

<style scoped>
	header {
		display: flex;
		justify-content: center;
	}
	.logo {
		width: 15.625rem;
		margin-top: 2rem;
	}
</style>
