<template>
	<div class="not-found">
		<h1>404</h1>
		<p>{{ notFoundMsg }}</p>
	</div>
</template>

<script>
	export default {
		name: "PageNotFound",
		/*eslint-disable */
		computed: {
			notFoundMsg() {
				if (this.language === "en") {
					return "Page not found";
				}
				if (this.language === "es") {
					return "La página no ha sido encontrada";
				}
			},
		},
		/*eslint-enable */
		props: {
			language: {
				type: String,
				default: "en",
			},
		},
	};
</script>

<style scoped>
	.not-found {
		display: flex;
		align-items: center;
		flex-direction: column;
		margin-top: 4rem;
		color: black;
	}
</style>
