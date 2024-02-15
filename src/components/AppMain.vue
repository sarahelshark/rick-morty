<script>
import axios from "axios";
import CharacterItem from "./CharacterItem.vue";
import LoadingIcon from "./LoadingIcon.vue";
import ResultsFilter from "./ResultsFilter.vue";
export default {
  name: "AppMain",
  components: {
    CharacterItem,
    LoadingIcon,
    ResultsFilter
},
  data() {
    return {
      base_api_url: "https://rickandmortyapi.com/api/character",
      characters: [],
      loading: true,
      error: false,
      searchText:'',
      selectedStatus:'',
    };
  },
  methods: {
    getCharacters(url) {
      axios
        .get(url)
        .then((response) => {
          console.log(response);
          console.log(response.data); // All data including pagination info
          console.log(response.data.results); // Only characters results
          //console.log(this);
          this.characters = response.data;
          this.loading = false;
          //reset the error massage to false if on the
          //previous call we got an error
          this.error = false;
        })
        .catch((error) => {
          console.error(error.response.data.error);
          this.error = error.response.data.error;
        });
    },
    filterResults(data){
      //?name=rick&status=alive
      console.log('filtered', data);
      //uso destructuring
      const [searchText, selectedStatus] = data ;

      const url = `${this.base_api_url}?name=${searchText}&status=${selectedStatus}`;
      console.log(url);

      this.getCharacters(url);
    },
  },
  computed: {
    getResults() {
      //console.log(this.characters);
      return this.characters.results
        ? "Total results:" + this.characters.results.length
        : "no results yet"; // 20
    },
  },
  created() {
    this.getCharacters(this.base_api_url);

    // Use a timeout to test your loading icon
    // the timeout is used for slow down the request and
    // simulate a slow network request
    // disable the time out once the loader is ready
    /*     setTimeout(() => {
      this.getCharacters(this.base_api_url)

    }, 3000) */
  },
};
</script>

<template>
  <main>
    <div class="container">

      <ResultsFilter @filtered="filterResults"></ResultsFilter>

       <div v-if="error" style="color:red;"> {{ error }}</div>

      <div class="row" v-if="!loading">
        <CharacterItem
          v-for="character in characters.results"
          :key="character.id + '_character'"
          :character="character"
        >
        </CharacterItem>
      </div>
      <!-- /.row -->
      <LoadingIcon v-else></LoadingIcon>

      <div>
        {{ getResults }}
      </div>
    </div>
    <!-- /.container -->
  </main>
</template>

<style scoped></style>
