<template>

  <div class="movies-index">
    <div v-for="movie in movies">
      <h2> {{ movie.title }} </h2>
      <p> {{ movie.year }} </p>
      <p>Plot: {{ movie.plot }} </p>
      <router-link :to="`/movies/${movie.id}`">More Info</router-link>
    </div>
  </div>



</template>

<style>
</style>

<script>
import axios from "axios"

export default {
  data: function() {
    return {
      movies: [],
    };
  },
  created: function() {
    axios.get("/api/movies").then(response => {
      console.log(response.data);
      this.movies = response.data
    })
  },
  methods: {}
};
</script>