<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <div v-for="(pokemon, index) in pokemons" :key="index">
      <Pokemon :name="pokemon.name" :url="pokemon.url"/>
    </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon';

export default {
  name: 'App',
  components: {
    Pokemon
  },
  data() {
    return {
      pokemons: []
    }
  },
  created: function() {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0')
      .then(resolve => {
        this.pokemons = resolve.data.results;
        console.log(this.pokemons)
      })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
