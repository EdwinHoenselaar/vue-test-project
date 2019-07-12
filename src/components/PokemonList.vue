<template>
  <div>
    <div v-for="pokemon in pokemons" v-bind:key="pokemon.name" class="list-group">
      <button @click="$emit('pass-url', pokemon.url)" class="list-group-item list-group-item-action">{{pokemon.name}}</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "PokemonList",
  props: ["pokemons"],
  methods: {
    changeCurrentPokemon(e) {
      e.preventdefault()


    }
  }
}
</script>
