<template>
	<div>
		<input class="filter" type="text" placeholder="Write a pokemon name" />
	</div>
</template>

<script>
	export default {
		name: "Filter",
	};
</script>

<style scoped>
	.filter {
		width: 100%;
		outline: none;
		border: solid 1px rgb(248, 248, 248);
		border-radius: 5px;
		padding: 1rem 2.5rem 1rem 1rem;
		font-size: 1rem;
		box-shadow: 0 2px 2px rgba(0, 0, 0, 0.1), 0 5px 5px rgba(0, 0, 0, 0.1);
		margin-top: 2rem;
	}
	.filter:focus {
		background-color: lightyellow;
	}
</style>
