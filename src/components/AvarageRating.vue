<script setup>
import { computed, ref } from "vue";

const props = defineProps(["movies"]);

const avarageRating = computed(() => {
  const ratingSum = props.movies
    .map((m) => m.score)
    .reduce((acc, current) => parseInt(acc) + parseInt(current));

  return ((ratingSum / props.movies.length / 100) * 5).toFixed(1);
});
</script>

<template>
  <div
    class="d-inline-block px-2"
    data-bs-toggle="tooltip"
    data-bs-placement="top"
    :data-bs-title="
      'The avarage of all movies rating, ' +
      (avarageRating < 3.5
        ? 'Please try to find better movies to watch.'
        : 'Great! keep it up, you have a sick collection')
    "
  >
    <img src="../../src/assets/star.svg" alt="" /> {{ avarageRating }}
  </div>
</template>

<style scoped>
.search input.form-control {
  background: #0d161e !important;
  border: none !important;
  height: 48px;
  color: #fff;
}

.search input.form-control:focus {
  box-shadow: 100px 0 500px -2px #000;
  z-index: 9;
}
</style>
