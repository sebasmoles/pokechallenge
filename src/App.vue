<template>
	<div class="container">
		<Header />
		<Filter :language="language" />
		<router-view :language="language" />
		<Languages @change-language="changeLanguage" />
	</div>
</template>

<script>
	import Header from "./components/ui/Header.vue";
	import Filter from "./components/ui/Filter.vue";
	import Languages from "./components/ui/Languages.vue";

	export default {
		name: "App",
		components: {
			Header,
			Filter,
			Languages,
		},
		data() {
			return {
				language: "en",
			};
		},
		methods: {
			changeLanguage(language) {
				this.language = language;
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
