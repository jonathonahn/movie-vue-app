<template>
  <div class="movies-show">
    <h1>{{ movie.title }}</h1>
    <p>{{ movie.year }}</p>
    <p>{{ movie.plot }}</p>
    <h5>Actors:</h5>
    <p v-for="actor in movie.actors" v-bind:key="actor.id">
      {{ actor.first_name }} {{ actor.last_name }}
    </p>
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
