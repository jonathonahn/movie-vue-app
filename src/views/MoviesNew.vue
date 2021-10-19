<template>
  <div class="movies-new">
    <!-- aasdf -->
    <form action="http://localhost:3000/movies" target="_blank" method="post">
      <label for="title"> Title (required): </label>
      <input
        id="title"
        type="text"
        name="title"
        v-model="newMovieParams.title"
      />
      <br />
      <label for="year"> Year (optional): </label>
      <input id="year" type="text" name="year" v-model="newMovieParams.year" />
      <br />
      <label for="plot"> Plot (optional): </label
      ><textarea
        id="plot"
        type="text"
        name="plot"
        v-model="newMovieParams.plot"
      /><span v-if="newMovieParams.plot.length > 0"
        >Character limit: {{ 30000 - newMovieParams.plot.length }}</span
      >
      <br />
      <button v-on:click="createMovie()">Submit</button>
      <input type="submit" value="Post and View Data" />
    </form>
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
    clearFields: function () {
      this.newMovieParams.title = "";
      this.newMovieParams.year = null;
      this.newMovieParams.plot = "";
    },
  },
};
</script>

<style></style>
