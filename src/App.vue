<script>
 import axios from 'axios'
import Pokemon from './components/Pokemon.vue'

  export default{
  components: { Pokemon },
   name: 'App',
   data(){
    return {pokemons: [] ,
     search:''
  }},
   created: function(){
     axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res =>{
       this.pokemons = res.data.results
       console.log(res.data.results)
     })
   },
   computed:{
     searchResult: function(){
       if(this.search == '' || this.search == ' '){
         return this.pokemons
       }else{
         return this.pokemons.filter(pokemon => pokemon.name == this.search)
       }
     }
   }
   
 }
</script>

<template>
  <div id="app">
    <div class="Top">
        <img class="pokeLogo" src="./assets/Poke.png" alt="" srcset="">
    <input v-model="search" id="Search" type="text" placeholder="Buscar Pokemon" class="input is-rounded "/>
    </div>
  
    <div class="columns is-desktop is-multiline ">
    <div v-for="(poke,index) in searchResult" :key="index">
       <Pokemon  class="column  " :name="poke.name.charAt(0).toUpperCase() + poke.name.slice(1)" :url="poke.url" :num="index+1"/>
    </div>
    </div>
    </div>
</template>

<style>
body{
  height: 100%;
  background-color: #1c2733;
}
.columns{
 justify-content: center;
}
.Top{
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
.pokeLogo{
  margin-top: 20px;
  width: 400px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  max-width: 3000px;
  background-color: #1c2733;
  height: 6000px;
}
#Search{
  width: 1000px;
  margin-top:30px;
}

</style>
  