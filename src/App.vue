<script>
import axios from "axios";
export default {
  name: "App",
  data() {
    return {
      base_api_url: "https://rickandmortyapi.com/api/character",
      characters: [],
      error: false,
    };
  },
  mounted() {
    //console.log(this.base_api_url);
    axios
      .get(this.base_api_url)
      .then((response) => {
        console.log(response.data); //all data including pagination info
        console.log(response.data.result); //only characters results
        console.log(this);
        this.characters = response.data;
      })
      .catch((error) => {
        console.error(error);
        this.error = error.message;
      });
  },
};
</script>
<template>
  <div v-for="character in characters.results" :key="character.id + '_character'">
   {{ character.name }}
   <img :src="character.image" alt=""/>
   {{ character.species}}
   {{ character.status }}
  </div>
</template>

<style scoped></style>
