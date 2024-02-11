<script>
import axios from "axios";
import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";
import AppFooter from "./components/AppFooter.vue";
export default {
  name: "App",
  components:{
    AppHeader,
    AppMain,
    AppFooter,
  },
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

  <AppHeader></AppHeader>
<AppMain></AppMain>
<AppFooter></AppFooter>
  <main>
    <div
      v-for="character in characters.results"
      :key="character.id + '_character'"
    >
      {{ character.name }}
      <img :src="character.image" alt="" />
      {{ character.species }}
      {{ character.status }}
    </div>
  </main>

  <footer></footer>
</template>

<style scoped></style>
