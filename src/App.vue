<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <div v-for="(poke, index) in pokemons" :key="index">
        <Pokemon :name="poke.name" :num="index+1"/>
      </div>
    </div>
   
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from "./components/Pokemon"
export default {
  name: 'App',
  data(){
    return{
      pokemons: []
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then( resp =>{
      this.pokemons = resp.data.results;

    })
  },
  components:{
    Pokemon
  }

}
</script>

<style>
#app{
  text-align: center;
}
</style>
