<template>
	<Pokemon :key="$route.params.name" />
</template>

<script>
	import Pokemon from "../components/Pokemon.vue";

	export default {
		name: "About",
		components: {
			Pokemon,
		},
	};
</script>
