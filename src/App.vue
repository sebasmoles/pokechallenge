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
		background-color: #ff3c3c;
		font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
	}
	.container {
		max-width: 500px;
		margin: 30px auto;
		overflow: auto;
		padding: 10px;
	}
</style>
