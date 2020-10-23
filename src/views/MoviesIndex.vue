<template>
  <div class="movies-index">
    <div>
      <button>Sort Alphabetically</button>
    </div>
    Search by name: <input v-model="titleFilter" list="titles" />
    <datalist id="titles">
      <option v-for="movie in movies">{{ movie.title }}</option>
    </datalist>
    Search by Title: <input v-model="titleFilter" />
    <div
      v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), 'title')"
    >
      <!-- <div v-for="movie in filterBy(movies, titleFilter, 'title')"> -->
      <!-- <div v-for="movie in movies"> -->
      <h2>{{ movie.title }}</h2>
      <p>{{ movie.year }}</p>
      <p>Plot: {{ movie.plot }}</p>
      <router-link :to="`/movies/${movie.id}`">More Info</router-link>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      movies: [],
      titleFilter: "",
    };
  },
  created: function() {
    axios.get("/api/movies").then((response) => {
      console.log(response.data);
      this.movies = response.data;
    });
  },
  methods: {},
};
</script>
