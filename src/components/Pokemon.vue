<template>
  <div>
    
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: "Pokemon",
  props: ["currentPokemonUrl"],
  created() {
    if(currentPokemonUrl !== "") {
      axios.get(currentPokemonUrl)
        .then(res => console.log("pokemon response test" ,res))
        .catch(err => console.error(err))
    }
  },
  data() {
    return {
      currentPokemon: {}
    }
  }
  
}
</script>

<style scoped>

</style>

