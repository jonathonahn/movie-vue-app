<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div>Title: <input type="text" v-model="newMovieParams.title" /></div>
    <div>Year: <input type="text" v-model="newMovieParams.year" /></div>
    <div>Plot: <input type="text" v-model="newMovieParams.plot" /></div>
    <div>Director: <input type="text" v-model="newMovieParams.director" /></div>
    <button v-on:click="createMovie()">Create Movie</button>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <p>{{ movie }}</p>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      movies: [],
      newMovieParams: {},
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("http://localhost:3000/movies").then((response) => {
        this.movies = response.data;
      });
    },
    createMovie: function () {
      var params = this.newMovieParams;
      axios
        .post("http://localhost:3000/movies", params)
        .then((response) => {
          this.movies.push(response.data);
          this.newMovieParams.title = "";
          this.newMovieParams.year = "";
          this.newMovieParams.plot = "";
          this.newMovieParams.director = "";
        })
        .catch((error) => {
          console.log(error.response.data.errors);
        });
    },
  },
};
</script>
