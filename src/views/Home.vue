<template>
	<Pokedex :language="language" />
</template>

<script>
	import Pokedex from "../components/Pokedex.vue";

	export default {
		name: "Home",
		props: {
			language: {
				type: String,
				default: "en",
			},
		},
		components: {
			Pokedex,
		},
	};
</script>
