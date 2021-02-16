<template>
  <div class="movies-show">
    <h1>Title: {{ movie.title }}</h1>
    <router-link :to="`/movies/${movie.id}/edit`">
      <button>Edit</button>
    </router-link>
    <button v-on:click="destroyMovie()">Delete</button>
    <br />
    <br />
    <img :src="movie.image" alt="" />
    <p>Year: {{ movie.year }}</p>
    <p>Director: {{ movie.director }}</p>
    <p>Plot: {{ movie.plot }}</p>
    <p>English: {{ movie.english }}</p>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      movie: {},
    };
  },
  created: function() {
    axios.get(`/api/movies/${this.$route.params.id}`).then(response => {
      this.movie = response.data;
      console.log(this.movie);
    });
  },
  methods: {
    destroyMovie: function() {
      if (confirm("Are you sure?")) {
        axios.delete(`/api/movies/${this.movie.id}`).then(response => {
          console.log(response.data);
          this.$router.push("/movies");
        });
      }
    },
  },
};
</script>
