<template>
	<div class="view-container">
		<Filter :placeholder="'Search'" id="filter" @input-event="(inputValue) => filterPokemons(inputValue)" />
		<div class="pokemon-card-container">
			<PokemonCard class="card" v-for="pokemon of pokemonsFiltred" 
      :pokemon="pokemon.name" 
      :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${getPokemonId(pokemon)}.png`"
      :id="`${getPokemonId(pokemon)}`"/>
		</div>
	</div>
</template>

<script>
import { defineComponent } from 'vue';
import PokemonCard from '@/components/PokemonCard.vue';
import Filter from '@/components/Filter.vue';

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
  },

  getPokemonId(pokemon) {
    return Number(pokemon.url.split("/")[6]);
  }
},

mounted() {
	fetch(URL)
  .then(response => response.json())
  .then(response => {
    this.pokemonsList = response.results;
    this.pokemonsFiltred = response.results;
  })
},

});
</script>

<style lang="scss">
  .view-container {
		display: flex;
		flex-direction: column;
		height: 100%;
    margin: 0 8px;
		#filter {
			margin: 16px 8px 12px 8px;
		}
		.pokemon-card-container {
			display: flex;
			flex-direction: row;
			flex-wrap: wrap;
      justify-content: center;
      min-width: 283px;
			.card {
        margin: 0 8px 16px 8px;
      }
		}
	}
</style>
