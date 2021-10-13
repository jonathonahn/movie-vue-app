<template>
  <div class="movies-new">
    <!-- aasdf -->
    Title (required): <input type="text" v-model="newMovieParams.title" />
    <br />
    Year (optional): <input type="text" v-model="newMovieParams.year" />
    <br />
    Plot (optional): <input type="text" v-model="newMovieParams.plot" /><span
      v-if="newMovieParams.plot.length > 0"
      >Character limit: {{ 30000 - newMovieParams.plot.length }}</span
    >
    <br />
    <button v-on:click="createMovie()">Submit</button>
    <br />
    <p v-if="!(errors.length === 0)">{{ errors }}</p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newMovieParams: { plot: "" },
      errors: [],
    };
  },
  created: function () {},
  methods: {
    createMovie: function () {
      this.errors = [];
      var params = this.newMovieParams;
      axios
        .post("/movies", params)
        .then((response) => {
          console.log(response);
          this.newMovieParams.title = "";
          this.newMovieParams.year = 0;
          this.newMovieParams.plot = "";
        })
        .catch((error) => {
          console.log(error.response.data.errors);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<style></style>
