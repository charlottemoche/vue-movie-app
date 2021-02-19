<template>
  <div class="movies-index">
    <myComponent @mouseover.native="hover = true" @mouseleave.native="hover = false" />
    <h1>Movies</h1>
    <div>
      Search:
      <input type="text" v-model="filter" list="titles" />
      <datalist id="titles">
        <option v-for="movie in movies" v-bind:key="movie.title">{{ movie.title }}</option>
      </datalist>
      <div>
        <button v-on:click="sortAttribute = 'title'">
          Sort alphabetically
        </button>
        <button v-on:click="sortAttribute = 'year'">
          Sort by year
        </button>
        <br />
      </div>
      <br />
      <div v-for="movie in orderBy(filterBy(movies, filter), sortAttribute)" v-bind:key="movie.id">
        <router-link :to="`/movies/${movie.id}`">
          <span>
            <img :src="movie.image" alt="" class="colortobw" />
          </span>
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
  </div>
</template>

<style scoped>
span:hover {
  background: #42b983;
}
</style>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      movies: [],
      filter: "",
      sortAttribute: "",
      hover: false,
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
