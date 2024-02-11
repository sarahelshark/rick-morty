<script>
import axios from "axios";
export default {
  name: "App",
  data() {
    return {
      base_api_url:'https://rickandmortyapi.com/api/character',
      characters: null
    };
  },
  mounted() {
    //console.log(this.base_api_url);
    axios
    .get(this.base_api_url)
    .then((response)=>{
      console.log(response.data);//all data including pagination info
      console.log(response.data.result);//only characters results
      console.log(this);
      this.characters = response.data;
    })
    .catch((error) => {
       console.error(error);
    })
    
  },
};
</script>
<template>
  <div></div>
</template>

<style scoped></style>
