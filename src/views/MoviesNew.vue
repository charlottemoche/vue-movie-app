<template>
  <div class="movies-new">
    <form v-on:submit.prevent="createMovie()">
      <h1>New Movie</h1>
      <p class="red-text" v-if="!$parent.isLoggedIn()">You must log in to add a new movie!</p>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>Title:</label>
        <input type="text" class="form-control" v-model="title" />
      </div>
      <br />
      <div class="form-group">
        <label>Year:</label>
        <input type="text" class="form-control" v-model="year" />
      </div>
      <br />
      <div class="form-group">
        <label>Plot:</label>
        <input type="text" class="form-control" v-model="plot" />
        <br />
        <small v-bind:class="{ 'red-text': plot.length > 100 }">{{ 100 - plot.length }} characters left</small>
        <small v-if="plot.length < 0" class="red-text"></small>
      </div>
      <div class="form-group">
        <label>Director:</label>
        <input type="text" class="form-control" v-model="director" />
      </div>
      <br />
      <div class="form-group">
        <label>English:</label>
        <input type="text" class="form-control" v-model="english" />
      </div>
      <br />
      <div class="form-group">
        <label>Image:</label>
        <input type="text" class="form-control" v-model="image" />
      </div>
      <br />
      <input type="submit" class="btn btn-primary" value="Create" />
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
