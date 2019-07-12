<template>
  <div>
    <p>ID: {{currentPokemon.id}}</p>
    <p>Name: {{currentPokemon.name}}</p>
    <p>Type: {{currentPokemon.type}}</p>
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
      console.log('watch test: ', newVal, oldVal)
      axios.get(newVal)
        .then(res => this.currentPokemon = res.data)
        .catch(err => console.error(err))
    }
  },
  data() {
    return {
      currentPokemon: {},
    }
  }
  
}
</script>

<style scoped>

</style>

