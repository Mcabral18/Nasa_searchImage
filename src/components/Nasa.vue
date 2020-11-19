<template>
  <div class="nasa">
    <form v-on:submit.enter.prevent="searchImage">
      <div class="row">
        <div class="four">
          <input
            class="u-full-width"
            type="text"
            placeholder="Search Image"
            v-model="searchQuery"
          />
        </div>
      </div>
    </form>
    <div v-for="nasa in nasa" :key="nasa.id">
      <img :src="nasa.links[0].href" alt="" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      searchQuery: "",
      nasa: [],
    };
  },
  methods: {
    async searchImage() {
      axios
        .get(
          `https://images-api.nasa.gov/search?q=${this.searchQuery} + '&media_type=image`
        )
        .then((response) => (this.nasa = response.data.collection.items));
      console.log(this.nasa);
    },
  },
};
</script>

<style scoped>
.four {
  display: block;
  margin: 2rem auto;
}
</style>
