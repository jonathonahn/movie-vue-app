<template>
  <div class="movies-index">
    <h1>{{ message }}</h1>
    Search by title: <input v-model="titleFilter" list="titles" />
    <datalist id="titles">
      <option v-for="movie in movies" v-bind:key="movie.id">
        {{ movie.title }}
      </option>
    </datalist>
    <div>
      <button v-on:click="setSortAttribute('title')">
        Sort Alphabetically
      </button>
      <button v-on:click="setSortAttribute('year')">Sort by Year</button>
    </div>
    <div
      v-for="movie in orderBy(
        filterBy(movies, titleFilter, 'title'),
        sortAttribute,
        sortOrder
      )"
      v-bind:key="movie.id"
    >
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
import Vue2Filters from "vue2-filters";
export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      message: "Movies",
      movies: [],
      titleFilter: "",
      sortAttribute: "title",
      sortOrder: 1,
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
    setSortAttribute: function (attribute) {
      if (this.sortAttribute === attribute) {
        this.sortOrder = this.sortOrder * -1;
      } else {
        this.sortAttribute = attribute;
        this.sortOrder = 1;
      }
    },
  },
};
</script>
