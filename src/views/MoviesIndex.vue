<template>
  <div class="movies-index">
    <h2>Movies</h2>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <router-link :to="`/movies/${movie.id}`">
        <img :src="movie.image" alt="" />
      </router-link>
      <p>Title: {{ movie.title }}</p>
      <p>Year: {{ movie.year }}</p>
      <p>Director: {{ movie.director }}</p>
      <p>Plot: {{ movie.plot }}</p>
      <p>English: {{ movie.english }}</p>
      <br />
      <router-link :to="`/movies/${movie.id}`"></router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      movies: [],
    };
  },
  created: function() {
    this.indexMovies();
  },

  methods: {
    indexMovies: function() {
      axios.get("/api/movies").then(response => {
        console.log(response.data);
        this.movies = response.data;
      });
    },
  },
};
</script>