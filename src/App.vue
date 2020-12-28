<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/pokeshelf.png">
      <h1 class="title">Poke<span>dex</span></h1>
      <input class="input is-rounded" type="text" placeholder="Buscar Pokemon Pelo Nome" v-model="busca">
      <button class="button is-fullwidth is-success" id="buscaBtn" @click="buscar">Buscar</button>
      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
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
      pokemons:[],
      filteredPokemons: [],
      busca: ''
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then( res =>{
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;

    })
  },
  components:{
    Pokemon
  },
  methods:{
    buscar: function(){
      this.filteredPokemons = this.pokemons;
       if(this.busca == '' || this.busca == ' ') {
         this.filteredPokemons = this.pokemons
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }
    }
}
</script>

<style>
#app{
  text-align: center;
}
.title{
  letter-spacing: 1px;
}
span{

  color: rgb(238, 38, 38);
}
#buscaBtn{
  margin-top: 10px;
}
</style>
