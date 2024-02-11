<script>
import axios from "axios";
export default {
  name: "App",
  data() {
    return {
      base_api_url:'https://rickandmortyapi.com/api/character',
    };
  },
  mounted() {
    //console.log(this.base_api_url);
    axios
    .get(this.base_api_url)
    .then((response)=>{
      console.log(response);
    })
    
  },
};
</script>
<template>
  <div></div>
</template>

<style scoped></style>
