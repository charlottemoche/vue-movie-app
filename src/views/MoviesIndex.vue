<template>
  <div class="movies-index">
    <h1>Movies</h1>
    Search:
    <input type="text" v-model="filter" list="titles" />
    <datalist id="titles">
      <option v-for="movie in movies" v-bind:key="movie.title">{{ movie.title }}</option>
    </datalist>
    <button v-on:click="sortAttribute = 'title'">Sort alphabetically</button>
    <button v-on:click="sortAttribute = 'year'">Sort by year</button>
    <br />
    <br />
    <div class="products-index">
      <div class="center">
        <div class="col mb-4">
          <div class="row row-cols-1 row-cols-md-3">
            <div v-for="movie in orderBy(filterBy(movies, filter), sortAttribute)" v-bind:key="movie.id">
              <router-link :to="`/movies/${movie.id}`">
                <span>
                  <img :src="movie.image" alt="" />
                </span>
              </router-link>
              <div class="card-body">
                <h5 class="card-title">{{ movie.title }}</h5>
                <p class="card-text">{{ movie.year }}</p>
                <p class="card-text">
                  {{ movie.director }}
                </p>
                <p class="card-text">
                  {{ movie.plot }}
                </p>
                <router-link :to="`/movies/${movie.id}`"></router-link>
              </div>
            </div>
          </div>
        </div>
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
