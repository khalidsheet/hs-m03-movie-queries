<script setup>
import { computed } from "@vue/reactivity";

const props = defineProps(["movie"]);

const movieScore = computed(() => ((props.movie.score / 100) * 5).toFixed(1));
</script>

<template>
  <div class="container">
    <div class="card bg-transparent">
      <div class="card-text">
        <img
          :src="movie.picture || './src/assets/poster-not-found.png'"
          :alt="`${movie.title}'s Poster Image`"
          class="card-image img-fluid"
        />
      </div>
      <div
        class="card-text mt-2"
        data-bs-toggle="tooltip"
        data-bs-placement="top"
        :data-bs-title="movie.title"
      >
        <div class="row">
          <div class="col-8 text-truncate">
            {{ movie.title }}
          </div>
          <div class="col-4 text-end">
            <img src="../../src/assets/star.svg" alt="" />
            {{ movieScore }}
          </div>
        </div>
      </div>
      <div class="card-text text-muted">
        <i class="bi bi-bookmark"></i>
        {{ movie.genre.toLowerCase() }}
        <span class="dot"></span>
        {{ movie.year }}
      </div>
    </div>
  </div>
</template>

<style scoped>
.card-image {
  width: 100%;
  height: 375px;
  max-height: 375px !important;
  border-radius: 20px;
}

span.dot {
  width: 5px;
  height: 5px;
  display: inline-block;
  background: #444;
  border-radius: 10px;
  margin-bottom: 2.5px;
  margin-left: 2.5px;
  margin-right: 2.5px;
}
</style>
