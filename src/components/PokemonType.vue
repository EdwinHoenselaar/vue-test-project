<template>
  <div class="col">
    <div v-for="type in types" v-bind:key="type.name" class="row">
      <input type="checkbox" :id="type.name" :value="type.name" v-model="checkedTypes" >
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
      pokemonListByTypes: [],
    }
  },
  methods: {
    removeDuplicates(originalArray, prop) {
     var newArray = [];
     var lookupObject  = {};

     for(var i in originalArray) {
        lookupObject[originalArray[i][prop]] = originalArray[i];
     }

     for(i in lookupObject) {
         newArray.push(lookupObject[i]);
     }
      return newArray;
    }
  },
  created() {
    axios.get("http://pokeapi.co/api/v2/type/")
      .then(res => {
        this.types = res.data.results
        })
      .catch(err => console.error(err))
  },
  watch: {
    checkedTypes: function getPokemonByTypes() {
      this.pokemonListByTypes = []
      this.checkedTypes.map(type => {
        axios.get(`http://pokeapi.co/api/v2/type/${type}`)
          .then(res => {
            const arrayWithoutKeys = res.data.pokemon.map(pokemon => {
              const object = {
                name: pokemon.pokemon.name,
                url: pokemon.pokemon.url
              }
              return object
            })
            const tempArray = [...this.pokemonListByTypes, ...arrayWithoutKeys]
            const filteredArray = this.removeDuplicates(tempArray, "name")
            this.pokemonListByTypes = filteredArray
            this.$emit('new-list', this.pokemonListByTypes);
          })
          .catch(err => console.error(err))
      })
    }
  }
  }
</script>



