<template>
	<div class="view-container">
		<Filter :placeholder="'Search'" id="filter" @input-event="(filtreds) => searchPokemons = filtreds" />
		<div class="pokemon-card-container">
			<PokemonCard v-for="pokemon of pokemons" :pokemon="pokemon.name" ref="child"/>
		</div>
	</div>
</template>

<script>
import { defineComponent } from 'vue';
import PokemonCard from '@/components/PokemonCard.vue';
import Filter from '@/components/Filter.vue'; // @ is an alias to /src

const URL = 'https://pokeapi.co/api/v2/pokemon?limit=151&offset=0';


export default defineComponent({
  name: 'HomeView',
  components: {
    PokemonCard,
    Filter
},

data() {
	return {
		pokemons: [],
		searchPokemons: ''
	}
},

methods: {
	getInputValue() {
		this.searchPokemons =	this.$refs.child.searchPokemons
		console.log(this.searchPokemons)
	}
},


mounted() {
	fetch(URL)
  .then(response => response.json())
  .then(response => this.pokemons = response.results)
},

});
</script>

<style lang="scss">
  .view-container {
	  background-color: #ededed;
		display: flex;
		flex-direction: column;
		height: 100%;
		#filter {
			margin: 15px;
		}
		.pokemon-card-container {
			display: flex;
			flex-direction: row;
			flex-wrap: wrap;
			// width: 100%;
		}
	}
</style>
