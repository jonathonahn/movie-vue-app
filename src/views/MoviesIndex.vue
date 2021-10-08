<template>
  <div class="movies-index">
    <h1>{{ message }}</h1>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h2>{{ movie.title }}</h2>
      <p>{{ movie.year }}</p>
      <p>{{ movie.plot }}</p>
      <br />
      <router-link :to="`/movies/${movie.id}`">Go to movie</router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Movies",
      movies: [],
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("/movies").then((response) => {
        this.movies = response.data;
      });
    },
    showPost: function () {
      //asdf
      <router-link to="/moviesnew">New Movie</router-link>;
    },
  },
};
</script>
