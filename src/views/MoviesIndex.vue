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

    <div class="service-content" id="services">
      <div class="container">
        <div class="row">
          <div class="col-md-4">
            <div class="left-text">
              <h4>Movies Index</h4>
              <div class="line-dec"></div>
              <p>
                Here is a list of all the movies stored in this web app!
              </p>
              <ul>
                <li>- Praesent porta urna id eros</li>
                <li>- Curabitur consectetur malesuada</li>
                <li>- Nam pretium imperdiet enim</li>
                <li>- Sed viverra arcu non nisi efficitur</li>
              </ul>
              <div class="primary-button">
                <a href="#portfolio">Learn More About Us</a>
              </div>
            </div>
          </div>
          <div class="col-md-8">
            <div class="row">
              <div class="col-md-6">
                <div class="service-item">
                  <h4>Classic Modern Design</h4>
                  <div class="line-dec"></div>
                  <p>
                    Sed lacinia ligula est, at venenatis ex iaculis quis. Morbi
                    sollicitudin nulla eget odio pellentesque.
                  </p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
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
