<template>
	<div class="filter">
		<input v-model="searchPokemons" type="text" v-bind:placeholder="placeholder" @keydown="$emit('input-event', this.searchPokemons)">
	</div>
</template>

<script>
	export default {
		name: 'Filter',
		expose: ['searchPokemons'],
		props: {
			placeholder: String
		},

		data() {
			return {
				searchPokemons: ''
			}
		}
	}
</script>

<style lang="scss" scoped>
	.filter {
		display: flex;
		input {
			background: none;
			border: none;
			border-bottom: 1px solid #b9b9b9;
			height: 60px;
			min-width: 283px;
			outline: none;
			width: 100%;
		}
	}
</style>