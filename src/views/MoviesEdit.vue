<template>
  <div class="movies-edit">
    <h1>{{ message }}</h1>
    <h2>this is the movie:</h2>
    <div>{{ movie }}</div>
    Title: <input type="text" v-model="editMovieParams.title" />
    <br />
    Year: <input type="text" v-model="editMovieParams.year" />
    <br />
    Plot: <input type="text" v-model="editMovieParams.plot" />
    <br />
    <button v-on:click="updateMovie()">Send Edit</button>
    <br />
    <button v-on:click="deleteMovie()">Delete Movie</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "This is an edit page",
      movie: {},
      editMovieParams: {},
      errors: [],
    };
  },
  created: function () {
    axios.get(`/movies/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {
    updateMovie: function () {
      axios
        .patch(`/movies/${this.movie.id}`, this.editMovieParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push(`/movies/${response.data.id}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    deleteMovie: function () {
      if (confirm("Are you sure you want to delete this movie?")) {
        axios.delete(`/movies/${this.movie.id}`).then((response) => {
          console.log(response.data);
          this.$router.push("/movies");
        });
      }
    },
  },
};
</script>
