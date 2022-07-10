<template>
	<div class="view-container">
		<Filter :placeholder="'Search'" id="filter" @input-event="(inputValue) => filterPokemons(inputValue)" />
		<div class="pokemon-card-container">
			<PokemonCard v-for="pokemon of pokemonsFiltred" :pokemon="pokemon.name" />
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
		pokemonsList: [],
		inputValue: '',
    pokemonsFiltred: []
	}
},

methods: {
	filterPokemons(search) {
    this.inputValue = search.toLowerCase();

    this.pokemonsFiltred = this.pokemonsList.filter(({name}) => {
      return name.includes(this.inputValue);
    });
  }
},

mounted() {
	fetch(URL)
  .then(response => response.json())
  .then(response => {
    this.pokemonsList = response.results
    this.pokemonsFiltred = response.results
  })
},

});
</script>

<style lang="scss">
  .view-container {
	  // background-color: #ededed;
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
