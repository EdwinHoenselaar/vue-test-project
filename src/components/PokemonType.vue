<template>
  <div class="col">
    <div v-for="type in types" v-bind:key="type.name" class="row">
      <input type="checkbox" :id="type.name" :value="type.name" v-model="checkedTypes">
      <p>{{type.name}}</p>
    </div>
  </div>

</template>

<script>
import axios from 'axios'

export default {
  name: "PokemonType",
  data() {
    return {
      types: [],
      checkedTypes: [],
    }
  },
  created() {
    axios.get("http://pokeapi.co/api/v2/type/")
      .then(res => {
        this.types = res.data.results
        })
      .catch(err => console.error(err))
    },
  }
</script>



