<template>
	<div>
		<input
			class="filter"
			type="text"
			placeholder="Search a pokemon"
			autocomplete="off"
		/>
	</div>
</template>

<script>
	export default {
		name: "Filter",
	};
</script>

<style scoped>
	.filter {
		font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
			Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
		font-size: 1rem;
		width: 100%;
		outline: none;
		border: solid 1px rgb(248, 248, 248);
		border-radius: 5px;
		padding: 1rem 2.5rem 1rem 1rem;
		box-shadow: 0 2px 2px rgba(0, 0, 0, 0.1), 0 5px 5px rgba(0, 0, 0, 0.1);
		margin-top: 2rem;
	}
	.filter:focus {
		background-color: rgb(251, 251, 180);
	}
</style>
