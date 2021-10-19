<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Navbar</a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav">
            <li class="nav-item">
              <router-link class="nav-link active" aria-current="page" to="/">Home</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/movies">Movies</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/movies/new">New Movies</router-link>
            </li>
            <li v-if="isLoggedIn()" class="nav-item">
              <router-link class="nav-link" to="/logout">Logout</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/signup">Signup</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/login">Login</router-link>
            </li>
          </ul>
        </div>
      </div>
    </nav>
    <router-view />
  </div>
</template>

<style></style>

<script>
export default {
  data: function () {
    return {
      flashMessage: "",
    };
  },
  methods: {
    isLoggedIn: function () {
      return localStorage.getItem("jwt");
    },
  },
  isLoggedIn: function () {
    return localStorage.jwt;
  },
  getUserId: function () {
    return localStorage.user_id;
  },
};
</script>
