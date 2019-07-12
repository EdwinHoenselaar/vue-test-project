<template>
  <div id="app">
    <Header class="row justify-content-center"/>
    <PokemonList v-bind:pokemon="pokemon" class="col-4" v-on:pass-url="changeCurrentPokemon"/>
    <Pokemon class="col-8" v-bind:currentPokemonUrl="currentPokemonUrl"/>
  </div>
</template>

<script>
import PokemonList from './components/PokemonList'
import Header from './components/Header'
import Pokemon from './components/Pokemon'
import axios from 'axios'

export default {
  name: 'app',
  components: {
    PokemonList,
    Pokemon,
    Header
  },
  data() {
    return {
      pokemon:[],
      currentPokemonUrl: ''
    }
  },
  created() {
    axios.get("https://pokeapi.co/api/v2/pokemon/?offset=0&limit=150")
      .then(res => {
        console.log('response test: ', res.data)
        this.pokemon = res.data.results
        })
      .catch(err => console.error(err))
  },
  methods: {
    changeCurrentPokemon(url) {
      this.currentPokemonUrl = url
    }
  }
}
</script>

