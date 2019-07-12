<template>
  <div>
    <p>ID: {{currentPokemon.id}}</p>
    <p>Name: {{currentPokemon.name}}</p>
    <p>Types:</p>
    <div v-for="type in currentPokemon.types" v-bind:key="type.type.name">
      <p class="bold">{{type.type.name}}</p>
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
  .bold {
    color: red;
  }
</style>

