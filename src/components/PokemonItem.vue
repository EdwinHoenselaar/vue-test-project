<template>
  <div>
    <p>Name: {{poke.results.name}}</p>
    <!-- <p>Type: {{poke.type}}</p> -->
  </div>
</template>

<script>
export default {
  name: "PokemonItem",
  props: ["poke"]
}
</script>

<style scoped>

</style>
