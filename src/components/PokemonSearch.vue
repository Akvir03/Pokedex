<template>
  <div class="searchbar">
    <input type="text" placeholder="Pokemon à rechercher" v-model="nomrecherche">
  </div>
</template>

<script>
export default {
  props:["pokurl"],
  data: () => {
    return {
      nomrecherche:"",
    }
  },
  watch:{
    nomrecherche(nom){
      this.nomrecherche = nom;
      this.$emit("affichepok",nom);
    }
  }
};
</script>

<style scoped>
.searchbar {
  position: relative;
  width: 100%;
  max-width: 510px;
  padding-bottom: 20px;
}
input {
  border: none;
  outline: none;
  border-radius: 5px;
  padding: 10px 40px 10px 10px;
  width: calc(100% - 50px);
  font-size: 1rem;
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2), 0 10px 10px rgba(0, 0, 0, 0.2);
}
</style>
