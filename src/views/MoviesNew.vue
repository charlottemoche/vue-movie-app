<template>
  <div class="movies-new">
    <h1>New Movie</h1>
    <p class="red-text" v-if="!$parent.isLoggedIn()">You must log in to add a new movie!</p>
    <ul>
      <li class="text-danger" v-for="error in errors" v-bind:key="error">
        {{ error }}
      </li>
    </ul>
    <form v-on:submit.prevent="createMovie()">
      <label for="title">Title:</label>
      <input type="text" id="title" name="title" value="" v-model="title" />
      <br />
      <br />
      <label for="year">Year:</label>
      <input type="text" id="year" name="year" value="" v-model="year" />
      <br />
      <br />
      <label for="plot">Plot:</label>
      <input type="text" id="plot" name="plot" value="" v-model="plot" />
      <br />
      <small v-bind:class="{ 'red-text': plot.length > 100 }">{{ 100 - plot.length }} characters left</small>
      <small v-if="plot.length < 0" class="red-text"></small>
      <br />
      <br />
      <label for="year">Director:</label>
      <input type="text" id="director" name="director" value="" v-model="director" />
      <br />
      <br />
      <label for="english">English:</label>
      <input type="text" id="english" name="english" value="" v-model="english" />
      <br />
      <br />
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>
<style scoped>
.red-text {
  color: red;
}
</style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      title: "",
      year: "",
      plot: "",
      director: "",
      english: "",
      image: "",
      errors: [],
    };
  },
  methods: {
    createMovie: function() {
      var params = {
        title: this.title,
        year: this.year,
        plot: this.plot,
        director: this.director,
        english: this.english,
        image: this.image,
      };
      axios
        .post("/api/movies", params)
        .then(response => {
          console.log(response.data);
          this.$router.push("/movies");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
