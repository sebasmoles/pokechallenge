<template>
	<div class="container">
		<Header />
		<Filter />
		<router-view />
	</div>
</template>

<script>
	import Header from "./components/ui/Header.vue";
	import Filter from "./components/ui/Filter.vue";

	export default {
		components: {
			Header,
			Filter,
		},
	};
</script>

<style>
	* {
		box-sizing: border-box;
		margin: 0;
		padding: 0;
	}
	body {
		background-color: #00e2ab;
		font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
			Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
		font-size: 1rem;
	}
	.container {
		max-width: 500px;
		margin: 30px auto;
		overflow: auto;
		padding: 10px;
	}
</style>
