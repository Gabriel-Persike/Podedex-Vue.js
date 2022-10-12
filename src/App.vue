<template>
  <div id="app">
    <h2 class="is-size-4">Pokedex</h2>

    <div class="column is-half is-offset-one-quarter">
      <input type="text" name="" id="" placeholder="Nome" v-model="busca" class="input is-rounded">
        <button class="button is-fullwidth is-success" id="buscaBtn" @click="buscar">Buscar</button>
        <div v-for="(poke,index) in filteredPokemons" :key="poke.url">
          <PokemonComponent :name="poke.name" :url="poke.url" :num="index + 1"/>
      </div>
    </div>

  </div>
</template>

<script>
import axios from "axios";
import PokemonComponent from "./components/PokemonComponent.vue"


export default {
  name: 'App',
  data(){
    return{
      pokemons:[],
      filteredPokemons:[],
      busca:""
    }
  },  
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=150&offset=0").then(res=>{
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
    });
  },
  components: {
    PokemonComponent
  },
  computed:{
    /*resultadoBusca: function(){
      if (this.busca == "" || this.busca == " ") {
          return this.pokemons;
      }else{

        return this.pokemons.filter(pokemon=> pokemon.name.toUpperCase() == this.busca.toUpperCase());
      }
    }*/
  },
  methods:{
    buscar:function(){
      if (this.busca == "" || this.busca == " ") {
        this.filteredPokemons = this.pokemons;
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon=> pokemon.name.toUpperCase() == this.busca.toUpperCase());
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#buscaBtn{
  margin-top: 2%;
}
</style>
