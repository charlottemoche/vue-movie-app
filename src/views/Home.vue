<template>
  <div class="home">
    <h1>New Movie</h1>
    <div>
      <input type="text" v-model="newMovieTitle" placeholder="title" />
      <br />
      <br />
      <input type="text" v-model="newMovieYear" placeholder="year" />
      <br />
      <br />
      <input type="text" v-model="newMoviePlot" placeholder="plot" />
      <br />
      <br />
      <input type="text" v-model="newMovieDirector" placeholder="director" />
      <br />
      <br />
      <input type="text" v-model="newMovieEnglish" placeholder="english" />
      <br />
      <br />
      <input type="text" v-model="newMovieGenres" placeholder="genre" />
      <br />
      <br />
      <button v-on:click="createMovie()">Add a movie</button>
    </div>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h1>title: {{ movie.title }}</h1>
      <p>year: {{ movie.year }}</p>
      <p>plot: {{ movie.plot }}</p>
      <p>director: {{ movie.director }}</p>
      <p>english: {{ movie.english }}</p>
      <p>genre: {{ movie.genres }}</p>
    </div>
  </div>
</template>
<style></style>
<script>
import axios from "axios";
export default {
  data: function() {
    return {
      message: "Movies",
      movies: [],
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      newMovieDirector: "",
      newMovieEnglish: "",
      newMovieGenres: "",
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
    createMovie: function() {
      var params = {
        title: this.newMovieTitle,
        year: this.newMovieYear,
        plot: this.newMoviePlot,
        director: this.newMovieDirector,
        english: this.newMovieEnglish,
        genre: this.newMovieGenres,
      };
      axios
        .post("/api/movies", params)
        .then(response => {
          console.log(response.data);
          this.movies.unshift(response.data);
        })
        .catch(error => {
          console.log(error.response.data.errors);
        });
    },
  },
};
</script>
