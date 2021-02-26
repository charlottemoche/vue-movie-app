<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="/">Home</a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarNavAltMarkup"
        aria-controls="navbarNavAltMarkup"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
        <div class="navbar-nav">
          <router-link class="nav-link" to="/movies">Movies</router-link>
          <router-link class="nav-link" to="/movies/new">New Movie</router-link>
          <router-link class="nav-link" v-if="isLoggedIn()" to="/logout">Logout</router-link>
          <router-link class="nav-link" v-if="!isLoggedIn()" to="/signup">Signup</router-link>
          <router-link class="nav-link" v-if="!isLoggedIn()" to="/login">Login</router-link>
        </div>
      </div>
    </nav>
    <div class="container">
      <router-view />
    </div>
  </div>
</template>

<style>
img {
  width: 250px;
}
.center {
  text-align: center;
}
.container {
  padding-top: 50px;
  padding-right: 30px;
  padding-bottom: 50px;
  padding-left: 80px;
}
</style>

<script>
export default {
  methods: {
    isLoggedIn: function() {
      return localStorage.jwt;
    },
    getUserId: function() {
      return localStorage.user_id;
    },
  },
};
</script>
