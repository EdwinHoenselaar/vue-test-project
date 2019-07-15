<template>
  <div class="container poke-header">
    <div class="row">
      <img :src="getImgUrl()" />
      <h1 >Welkom bij de Apostle Pokemon app</h1>
      <img :src="getImgUrl()" />
    </div>
  </div>
</template>

<script>
export default {
  name: "Header",
  methods: {
    getImgUrl(){
      const random = Math.floor(Math.random() * 100) + 1
      return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${random}.png`
    }
  }
}
</script>

<style scoped>
  .poke-header {
    background: lightblue;
    color: red;
    border-bottom: 2px solid black;
    border-radius: 10px;
    padding:10px;
    margin: 20px auto;
  }
  h1 {
    margin: auto 10px;
  }
</style>


