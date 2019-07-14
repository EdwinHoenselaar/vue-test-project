<template>
  <div>
    <img :src="currentPokemon.sprites.front_default" />
    <h1># {{currentPokemon.id}} {{this.capitalize(currentPokemon.name)}}</h1>
    <p>Types:</p>
    <div v-for="type in currentPokemon.types" v-bind:key="type.type.name">
      <p class="red">{{type.type.name}}</p>
    </div>
    <p>Height: {{currentPokemon.height}}</p>
    <p>Weight: {{currentPokemon.weight}}</p>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: "Pokemon",
  props: ["currentPokemonUrl"],
  watch: {
    currentPokemonUrl: function getPokemon(newVal, oldVal) {
      axios.get(newVal)
        .then(res => {
          this.currentPokemon = res.data
        })
        .catch(err => console.error(err))
    }
  },
  methods: {
    capitalize (s) {
      if (typeof s !== 'string') return ''
      return s.charAt(0).toUpperCase() + s.slice(1)
    }
  },
  data() {
    return {
      currentPokemon: {},
    }
  },
  created() {
    axios.get(this.currentPokemonUrl)
      .then(res => {
        this.currentPokemon = res.data
      })
      .catch(err => console.error(err))  
  }
  
}
</script>

<style scoped>
  .red {
    color: red;
  }
</style>

