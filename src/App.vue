<template>
  <div id="app">
    <div class="fixed-side-navbar">
      <ul class="nav flex-column">
        <li class="nav-item">
          <a class="nav-link" href="/"><span>Home</span></a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="/about"><span>About</span></a>
        </li>
        <span v-if="isLoggedIn()">
          <li class="nav-item">
            <a class="nav-link" href="/logout"><span>Logout</span></a>
          </li>
        </span>
        <li class="nav-item">
          <a class="nav-link" href="/signup"><span>Signup</span></a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="/login"><span>Login</span></a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="/movies"><span>Movies Index</span></a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="/movies.new"><span>New Movie</span></a>
        </li>
      </ul>
    </div>

    <!-- Need to delete this whole div - just using it for reference right now -->
    <!-- <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> |
      <span v-if="isLoggedIn()">
        <router-link to="/logout">Logout</router-link> |
      </span>
      <span v-else>
        <router-link to="/signup">Signup</router-link> |
        <router-link to="/login">Login</router-link> |
      </span>
      <router-link to="/movies">Movies Index</router-link> |
      <router-link to="/movies/new">New Movie</router-link>
      <!-- <router-link to="`/movies/${movie.id}`">Movies Show</router-link> | -->
    <!-- </div> -->

    <router-view />

    <footer>
      <div class="container">
        <div class="row">
          <div class="col-md-12">
            <div class="primary-button">
              <a href="#home">Back To Top</a>
            </div>
            <ul>
              <li>
                <a href="#"><i class="fa fa-facebook"></i></a>
              </li>
              <li>
                <a href="#"><i class="fa fa-twitter"></i></a>
              </li>
              <li>
                <a href="#"><i class="fa fa-linkedin"></i></a>
              </li>
              <li>
                <a href="#"><i class="fa fa-google"></i></a>
              </li>
              <li>
                <a href="#"><i class="fa fa-dribbble"></i></a>
              </li>
            </ul>
            <p>
              Copyright &copy; 2019 Company Name - Design:
              <a rel="nofollow noopener" href="https://templatemo.com"
                ><em>TemplateMo</em></a
              >
            </p>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<style></style>

<script>
export default {
  data: function() {
    return {};
  },
  methods: {
    isLoggedIn: function() {
      return localStorage.getItem("jwt");
    },
    getUserId: function() {
      return parseInt(localStorage.getItem("user_id"));
    },
  },
};
</script>
