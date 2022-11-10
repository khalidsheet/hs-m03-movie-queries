<script setup>
import { computed, ref } from "vue";

const props = defineProps(["movies"]);
const selectedGenres = ref([]);

const genres = computed(() => {
  const genreSet = new Set();

  props.movies.filter((m) => {
    let g = m.genre.toLowerCase();
    g = g == "science fiction" ? "sci-fi" : g;

    genreSet.add(g);
  });

  return genreSet;
});
</script>

<template>
  <div class="row">
    <div class="col-12">
      <span class="fs-3 mb-3 d-block">Genres</span>
    </div>
    <div class="col-12">
      <div class="form-check" v-for="(genre, i) in genres" :key="i">
        <input
          class="form-check-input"
          type="checkbox"
          :value="genre"
          :id="i"
          v-model="selectedGenres"
          @change="$emit('filterChanged', selectedGenres.value)"
        />
        <label class="form-check-label" :for="i">
          {{ genre }}
        </label>
      </div>
    </div>
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
