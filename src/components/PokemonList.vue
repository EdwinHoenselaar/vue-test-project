<template>
  <div>
    <div v-for="poke in pokemon" v-bind:key="poke.name" class="list-group">
      <button class="list-group-item list-group-item-action">{{poke.name}}</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "PokemonList",
  props: ["pokemon"]
}
</script>
