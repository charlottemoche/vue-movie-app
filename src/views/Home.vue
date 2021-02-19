<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <router-link :to="`/movies`">
      <img :src="image" alt="" />
      <br />
      <button>See all movies</button>
    </router-link>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      message: "Charlotte's Favorite Movies",
      image: "https://pisces.bbystatic.com/image2/BestBuy_US/images/products/7745/7745586_so.jpg",
    };
  },
};
</script>
<style></style>
