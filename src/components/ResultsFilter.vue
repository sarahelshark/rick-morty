<script>
export default {
  name: "ResultsFilter",
  emits:['filtered'],
  data() {
    return {
      searchText: "",
      selectedStatus: "",
    };
  },
  methods: {
    /*filterResults() {
      console.log(this.searchText);
      console.log(this.selectedStatus);
      this.$emit('filtered' , [this.searchText, this.selectedStatus]);
    }, */
  },
};
</script>
<template>
  <div class="filters">
    <!-- add name filter input -->
    <input
      type="text"
      placeholder="Type a name to search"
      v-model="searchText"
    />
    <!-- add a select status filter -->
    <select name="status" id="status" v-model="selectedStatus">
      <option value="" selected>All</option>
      <option value="alive">Alive</option>
      <option value="dead">Dead</option>
      <option value="unknown">Unknown</option>
    </select>

    <!--<button @click="$emit('filtered', [searchText, selectedStatus])">
      filter now
    </button>-->
    <!--emit opzione 1, opzione 2 nel metodo in alto stesso, forse piu pratico! qui sotto:
        <button @click="filterResults()">filter now</button>
    -->
    <button @click="$emit('filtered',[searchText, selectedStatus])">
      filter now
    </button>
    
  </div>
</template>

<style></style>
