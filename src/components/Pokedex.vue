<template>
  <div class="container">
    <img src="https://upload.wikimedia.org/wikipedia/commons/9/98/International_Pok%C3%A9mon_logo.svg">
    <h1>Pokedex DEVIENNE Nathan BUT2 TPD</h1>
    <PokemonSearch PokemonSearch v-on:Search="recherche" @affichepok = "affpoke"/> 
    <PokemonDetail :pokurl = "envoie" :lienpoke="pokurl" v-if="verification" v-on:fermer="verification=false"/>
    <PokemonList v-on:affichepok = "update" :poke_search = "recherche"/> 
  </div>
</template>

<script>
import PokemonDetail from "../components/PokemonDetail.vue"; 
import PokemonList from "../components/PokemonList.vue";
import PokemonSearch from "../components/PokemonSearch.vue"; 

export default {
  components: {
    PokemonDetail, 
    PokemonList,
    PokemonSearch,
  },
  data: function(){
    return{
      verification: false,
      envoie: null,
      pokelist:[],
      pokurl:"https://pokeapi.co/api/v2/pokemon/",
      recherche:""
    };
  },
  methods:{
    update: function(poke){
      this.verification=true;
      this.envoie=poke;
    },
    affpoke(pokem){
      this.recherche = pokem;
    }
  }
};
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 10px;
  width: calc(100% - 20px);
  min-height: calc(100vh - 20px);
  //background: radial-gradient(#ffbf0b, #e20000);

  font-family: "Acme", arial;
  font-size: 1rem;
  font-weight: normal;
}

h1 {
  color: #efefef;
}
</style>