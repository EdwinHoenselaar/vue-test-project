<template>
  <div class="scrollbar">
    <div v-for="pokemon in pokemons" v-bind:key="pokemon.name" class="list-group">
      <button @click="$emit('pass-url', pokemon.url)" class="list-group-item list-group-item-action">{{pokemon.name}}</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "PokemonList",
  props: ["pokemons"],
}
</script>

<style scoped>
  .scrollbar {
    height: 80vh;
    overflow-y: scroll;
  }
</style>


