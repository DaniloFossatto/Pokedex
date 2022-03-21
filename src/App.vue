<script>
 import axios from 'axios'
import Pokemon from './components/Pokemon.vue'

  export default{
  components: { Pokemon },
   name: 'App',
   data(){
     pokemons: []
   },
   created: function(){
     axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res =>{
       this.pokemons = res.data.results
       
     })
   },
   
 }
</script>

<template>
  <div id="app">
    <img class="pokeLogo" src="./assets/Poke.png" alt="" srcset="">
    <div class="columns is-desktop is-multiline ">
    <div v-for="(poke,index) in pokemons" :key="index">
      <Pokemon  class="column  " :name="poke.name.charAt(0).toUpperCase() + poke.name.slice(1)" :url="poke.url" :num="index+1" />
    </div>
    </div>
    </div>
</template>

<style>
.columns{
 justify-content: center;
}
.pokeLogo{
  margin-top: 20px;
  margin-bottom: 100px;
  width: 500px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  max-width: 3000px;
  
}
</style>
  