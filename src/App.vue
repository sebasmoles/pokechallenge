<template>
	<div class="container">
		<Header />
		<Filter v-show="!isHidden" />
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
		data() {
			return {
				isHidden: false,
			};
		},
		watch: {
			$route: function () {
				// Check if given route is true, if so then hide filter component
				this.$route.path === "/about"
					? (this.isHidden = true)
					: (this.isHidden = false);
			},
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
		background-image: linear-gradient(rgb(255, 0, 0), white);
		font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
			Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
		font-size: 1rem;
		height: 100vh;
	}
	.container {
		max-width: 500px;
		margin: 30px auto;
		overflow: auto;
		padding: 10px;
	}
</style>
