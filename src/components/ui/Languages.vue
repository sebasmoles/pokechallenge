<template>
	<div class="languages">
		<select
			v-model="selectedLanguage"
			@change="onChange()"
			name="languages"
			id="languages"
		>
			<option value="en">English</option>
			<option value="es">Español</option>
		</select>
	</div>
</template>

<script>
	export default {
		name: "Languages",
		data() {
			return {
				selectedLanguage: "en",
			};
		},
		methods: {
			onChange() {
				this.$emit("change-language", this.selectedLanguage);
			},
		},
	};
</script>

<style scoped>
	.languages {
		display: flex;
		justify-content: center;
		margin-top: 2rem;
	}
	.languages select {
		font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
			Oxygen, Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
		padding: 0.5rem;
		width: 10rem;
		border-radius: 5px;
		border: 1px solid black;
		outline: none;
		box-shadow: 0 2px 2px rgba(0, 0, 0, 0.1), 0 5px 5px rgba(0, 0, 0, 0.1);
	}
</style>
