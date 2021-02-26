<template>
  <div class="home">
    <div class="jumbotron">
      <h1 class="display-4">My favorite movies!</h1>
      <p class="lead">
        This is a sample of some of my favorite movies
      </p>
      <hr class="my-4" />
      <img :src="image" alt="" />
      <br />
      <br />
      <router-link class="btn btn-primary btn-lg" :to="`/movies`" role="button">See all movies</router-link>
    </div>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      image: "https://pisces.bbystatic.com/image2/BestBuy_US/images/products/7745/7745586_so.jpg",
    };
  },
};
</script>
<style></style>
