<template>
  <div class="list">
    <article v-for="pokf in pokefiltre" :key="pokf.name" v-on:click="affichepok(pokf.url)">
        <h3>{{pokf.name}}</h3>
        <img :src="'https://img.pokemondb.net/sprites/bank/normal/'+pokf.name+'.png'"/>
    </article>
  </div>
</template>

<script>
import axios from 'axios';
import lodash from "lodash";
export default {
  props: ['poke_search'],
  name: "PokeList",
  data: function() {
    return {
      PokeList:[]
    }},

  computed:{
    pokefiltre: function(){
      if (this.poke_search.length==0){
        return this.PokeList;
      }
      else{
        let poke_search = this.poke_search.toLowerCase();
        return lodash.filter(this.PokeList, function(y) {
          return y.name.includes(poke_search);
        });
      }
    }
  },
    
  mounted (){
    axios
      .get("https://pokeapi.co/api/v2/pokemon?offset=0&limit=-1")
      .then(response => {
        this.PokeList = response.data.results
      }
      )
    },
  methods:{
    affichepok(poke){
      this.$emit('affichepok',poke);
    }
  }
};
</script>

<style lang="scss" scoped>
.list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  grid-gap: 10px;
  width: 100%;
  max-width: 510px;
}
article {
  height: 150px;
  background-color: #efefef;
  text-align: center;
  text-transform: capitalize;
  border-radius: 5px;
  cursor: pointer;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}
h3 {
  margin: 0;
}
#scroll-trigger {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 150px;
  font-size: 2rem;
  color: #efefef;
}

img {
  width: 96px;
  height: 96px;
}
</style>

