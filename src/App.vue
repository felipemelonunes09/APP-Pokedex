<template>
  <div id="app">
     
      <div class="column is-half is-offset-one-quarter">
        <input type="text" placeholder="Buscar pokemon pelo nome" v-model="busca" class="input is-rounded">
        <button class="button is-fullwidth buscarBtn is-success"> Pesquisar </button>
        <div v-for="(poke, index) in resultadoBusca" :key="index">
          <Pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
        </div>
      </div>
  </div>
</template>

<script>

import axios from 'axios'
import Pokemon from './components/Pokemon.vue'

export default {
  name: 'App',
  components: {
    Pokemon
  },
  data() {
    return {
      pokemons: [],
      busca: ''
    }
  },
  computed: {
    resultadoBusca: function () {
        if (this.busca == '' || this.busca == ' ') {
          return this.pokemons
        }
        else {
          return this.pokemons.filter(pokemon => pokemon.name == this.busca)
        }
    }
  },
  created: async function () {

    let res = await axios.get('https://pokeapi.co/api/v2/pokemon?limit=152&offset=0')
    this.pokemons = res.data.results
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

.buscarBtn {
  margin-top: 2%;
}

</style>
