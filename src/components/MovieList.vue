<script setup>
import Movie from "./Movie.vue";

defineProps(["movies"]);
// TODO:
</script>

<template>
  <div class="row g-4">
    <div
      class="col-lg-3 col-md-4 col-sm-6 col-xs-12"
      v-for="(movie, index) in movies"
      :key="index"
    >
      <Movie :movie="movie" />
    </div>
  </div>
</template>

<style scoped>
/* TODO: */
</style>
