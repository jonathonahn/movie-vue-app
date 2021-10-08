<template>
  <div class="movies-show">
    <h1>{{ message }}</h1>
    <h2>this is the movie:</h2>
    <div>{{ movie.title }}</div>
    <p>{{ movie.year }}</p>
    <p>{{ movie.plot }}</p>
    <br />
    <router-link :to="`/movies/${movie.id}/edit`">Edit</router-link>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "This is a show page",
      movie: {},
    };
  },
  created: function () {
    this.showMovie();
  },
  methods: {
    showMovie: function () {
      axios
        .get(`http://localhost:3000/movies/${this.$route.params.id}`)
        .then((response) => {
          this.movie = response.data;
        });
    },
  },
};
</script>
