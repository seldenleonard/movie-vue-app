<template>
  <div class="home">
    <h1>Movies</h1>
    
    <div v-for="movie in movies">
      <h2>Title: {{ movie.title }}</h2>
      <h4>Year: {{ movie.year }}</h4>
      <h4>Plot: {{ movie.plot }}</h4>
      <button v-on:click="showMovie(movie)">More Info</button>
    </div>
  
    <div>
      <h1>New Movie</h1>
      <li v-for="error in errors">{{ error }}</li>
      <ul>
        Title: <input type="text" v-model="newMovieTitle"><br>
        Year: <input type="text" v-model="newMovieYear"> <br>
        Plot: <input type="text" v-model="newMoviePlot"> <br>
        <button v-on:click="createMovie()">Create</button>
      </ul>
    </div>

    <dialog id="movie-details">
      <form method="dialog">
        <h2>Movie Info</h2>
        {{ currentMovie }}
        <p>Title: <input type="text" v-model="currentMovie.title"></p>
        <p>Year: <input type="text" v-model="currentMovie.year"></p>
        <p>Plot: <input type="text" v-model="currentMovie.plot"></p>
        <button v-on:click="updateMovie(currentMovie)">Update Movie</button>
        <button v-on:click="destroyMovie(currentMovie)">Destroy Movie</button>
        <button>Close</button>
      </form>
    </dialog>


  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movies: [],
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      currentMovie: {},
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("/api/movies").then((response) => {
        console.log(response.data);
        this.movies = response.data;
      });
    },
    createMovie: function () {
      var params = {
        title: this.newMovieTitle,
        year: this.newMovieYear,
        plot: this.newMoviePlot,
      };
      axios
        .post("/api/movies", params)
        .then((response) => {
          console.log("Success", response.data);
          this.movies = response.data; // I noticed after looking at Dani's code that I am missing several lines of code where I would begin with "this.movies.push(response.data)" and then list all the expected inputs and define them as empty strings. However, my code is working and the movie is getting entered into the database when I fill out the form. Is there any reason I should need those extra lines of code?
        })
        .catch((error) => {
          console.log(error.response.data.errors);
        });
    },
    showMovie: function (movie) {
      console.log(movie);
      this.currentMovie = movie;
      document.querySelector("#movie-details").showModal();
    },
    updateMovie: function (movie) {
      var params = {
        title: movie.title,
        year: movie.year,
        plot: movie.plot,
      };
      axios
        .patch(`/api/movies/${movie.id}`, params)
        .then((response) => {
          console.log("Success", response.data);
        })
        .catch((error) => {
          console.log(error.response.data.errors);
        });
    },
    destroyMovie: function (movie) {
      axios.delete(`/api/movies/${movie.id}`).then((response) => {
        console.log("Success", response.data);
        var index = this.movies.indexOf(movie);
        this.movies.splice(index, 1);
      });
    },
  },
};
</script>