<template>
  <div id="app">
    <Header class="row justify-content-center"/>
    <!-- <MyVuetable /> -->
    <div class="row">
      <PokemonList v-bind:pokemons="pokemons" class="col-4" v-on:pass-url="changeCurrentPokemon"/>
      <Pokemon class="col-4" v-bind:currentPokemonUrl="currentPokemonUrl"/>
      <PokemonType class="col-4" v-on:new-list="changeList"/>
    </div>
  </div>
</template>

<script>
import PokemonList from './components/PokemonList'
import MyVuetable from './components/MyVuetable'
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
    Header,
    MyVuetable
  },
  data() {
    return {
      pokemons:[],
      currentPokemonUrl: "https://pokeapi.co/api/v2/pokemon/1/",
      pokemonListByTypes: [],
      checkedTypes: [],
    }
  },
  created() {
    axios.get("https://pokeapi.co/api/v2/pokemon/?offset=0&limit=150")
      .then(res => {
        // console.log('response test: ', res.data)
        this.pokemons = res.data.results
        })
      .catch(err => console.error(err))
  },
  methods: {
    changeCurrentPokemon(url) {
      this.currentPokemonUrl = url
    },
    changeList(list) {
      console.log('list check before: ', this.pokemons)
      this.pokemons = list
      console.log('list check after: ', this.pokemons)
    }
  }
}
</script>

