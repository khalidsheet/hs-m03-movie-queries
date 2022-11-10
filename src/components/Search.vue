<script setup>
import { ref } from "vue";

const searchText = ref("");
</script>

<template>
  <div class="search px-2 mb-4">
    <input
      type="text"
      v-model="searchText"
      class="form-control"
      placeholder="Search"
      @input="$emit('searchChanged', searchText)"
    />
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
