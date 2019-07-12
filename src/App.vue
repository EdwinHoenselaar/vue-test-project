<template>
  <div id="app">
    <Header class="row justify-content-center"/>
    <div class="row">
      <PokemonList v-bind:pokemon="pokemon" class="col-4" v-on:pass-url="changeCurrentPokemon"/>
      <Pokemon class="col-4" v-bind:currentPokemonUrl="currentPokemonUrl"/>
      <PokemonType class="col-4" />
    </div>
  </div>
</template>

<script>
import PokemonList from './components/PokemonList'
import Header from './components/Header'
import Pokemon from './components/Pokemon'
import PokemonType from './components/PokemonType'
import axios from 'axios'

export default {
  name: 'app',
  components: {
    PokemonList,
    Pokemon,
    PokemonType,
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

