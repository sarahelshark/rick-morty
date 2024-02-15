<script>
import {store} from '../store.js';

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
      store, //store: store; versione non semplificata
      searchText:'',
      selectedStatus:'',
    };
  },
  methods: {
    
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
      return this.store.characters.results
        ? "Total results:" + this.store.characters.results.length
        : "no results yet"; // 20
    },
  },
  created() {
    this.store.getCharacters(this.store.base_api_url);

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

       <div v-if="store.error" style="color:red;"> {{ store.error }}</div>

      <div class="row" v-if="!store.loading">
        <CharacterItem
          v-for="character in store.characters.results"
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
