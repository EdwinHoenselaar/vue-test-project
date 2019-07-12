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
      this.checkedTypes.map(type => {
        axios.get(`http://pokeapi.co/api/v2/type/${type}`)
          .then(res => {
            const tempArray = [...this.pokemonListByTypes, ...res.data.pokemon]
            // const filteredArray = this.removeDuplicates(tempArray, "name")
            // console.log('filteredArray check: ', filteredArray)
            this.pokemonListByTypes = tempArray//filteredArray
            this.$emit('new-list', this.pokemonListByTypes);
          })
          .catch(err => console.error(err))
      })
    }
  }
  }
</script>



