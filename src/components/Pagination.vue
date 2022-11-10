<script setup>
import { computed, ref } from "@vue/runtime-core";

/**
 * so this component needs to know about the total elements and
 * chunk it into pages with a help from "itemsPerPage"
 */
const props = defineProps({
  movies: Array,
  itemsPerPage: Number,
});

const emit = defineEmits(["pageChanged"]);

const currentPage = ref(1);
const totalPages = computed(() => props.movies.length / props.itemsPerPage);

const paginationRules = computed(() => ({
  hasNextPage: currentPage.value < totalPages.value,
  hasPrevPage: currentPage.value - 1 != 0,
}));

const handleNextPage = () => {
  currentPage.value = currentPage.value + 1;
  emit("pageChanged", currentPage.value);
};

const handlePrevPage = () => {
  currentPage.value = currentPage.value - 1;
  emit("pageChanged", currentPage.value);
};

const handleFirstPage = () => {
  currentPage.value = 1;
  emit("pageChanged", currentPage.value);
};

const handleLastPage = () => {
  currentPage.value = totalPages.value;
  emit("pageChanged", currentPage.value);
};
</script>

<template>
  <div class="row">
    <div class="col-12">
      <div class="btn-group">
        <button
          class="btn btn-light ml-2"
          @click="handleFirstPage"
          :disabled="currentPage == 1 ? 'disabled' : null"
        >
          First
        </button>
        <button
          class="btn btn-light ml-2"
          :disabled="!paginationRules.hasPrevPage ? 'disabled' : null"
          @click="handlePrevPage"
        >
          Prev
        </button>
        <button class="btn btn-light ml-2" disabled="disabled">
          {{ currentPage }} / {{ totalPages }}
        </button>
        <button
          class="btn btn-light ml-2"
          @click="handleNextPage"
          :disabled="!paginationRules.hasNextPage ? 'disabled' : null"
        >
          Next
        </button>
        <button
          class="btn btn-light"
          @click="handleLastPage"
          :disabled="currentPage == totalPages ? 'disabled' : null"
        >
          Last
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* TODO: */
</style>
