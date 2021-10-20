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
    <div class="row row-cols-2 row-cols-md-3 g-4">
      <div
        class="col"
        v-for="movie in orderBy(
          filterBy(movies, titleFilter, 'title'),
          sortAttribute,
          sortOrder
        )"
        v-bind:key="movie.id"
      >
        <div class="card">
          <div class="card-body">
            <h5 class="card-title">{{ movie.title }}</h5>
            <p class="card-text">
              {{ movie.plot }}
            </p>
            <p v-for="actor in movie.actors" v-bind:key="actor.id">
              <img :src="actor.image" class="card-img-top" alt="actor image" />
            </p>
            <p>{{ movie.year }}</p>
            <router-link class="btn btn-primary" :to="`/movies/${movie.id}`"
              >Go to post</router-link
            >
          </div>
        </div>
      </div>
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
