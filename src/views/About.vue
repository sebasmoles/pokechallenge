<template>
	<Pokemon :key="$route.params.name" :language="language" />
</template>

<script>
	import Pokemon from "../components/Pokemon.vue";

	export default {
		name: "About",
		props: {
			language: {
				type: String,
				default: "en",
			},
		},
		components: {
			Pokemon,
		},
	};
</script>
