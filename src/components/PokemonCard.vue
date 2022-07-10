<template>
	<div class="pokemon-card" v-bind:id="id">
		<img v-bind:src="src">
		<div class="pokemon-information">
			<p>{{pokemon}}</p>
			<p>#{{id}}</p>
		</div>
	</div>
</template>

<script>
	export default {
		name: 'PokemonCard',
		props: {
			pokemon: String,
			id: Number,
			src: String
		},

	data() {
		return {
			url: 'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/'
		}
	}
}
</script>

<style lang="scss" scoped>
	.pokemon-card {
		align-items: center;
		background-color: #ffffff;
		border-radius: 4px;
		box-shadow: 0px 6px 7px 0px rgba(221,221,221,1);
		display: flex;
		flex-direction: column;
		height: 167px;
		justify-content: space-between;
		min-width: 268px;
		padding: 13px;
		width: 268px;
		img {
			height: 102px;
			width: 102px;
		}
		.pokemon-information {
			display: flex;
			flex-direction: row;
			justify-content: space-between;
			width: 100%;
			p {
				margin: 0;
			}
		}
	}	
</style>