<script setup>
import MovieList from "./components/MovieList.vue";
import Search from "./components/Search.vue";
import Pagination from "./components/Pagination.vue";
import Filters from "./components/Filters.vue";
import movies from "./assets/movies.json";
import { ref } from "@vue/reactivity";
import { nextTick } from "@vue/runtime-core";

const itemsPerPage = ref(10);
const paginatedMovies = ref(movies.slice(0, itemsPerPage.value));

const handleItemsPerPageChange = (evt) => {
  paginatedMovies.value = movies.slice(0, evt.target.value);
};

const handlePageChange = (page) => {
  paginatedMovies.value = movies.slice(
    (page - 1) * itemsPerPage.value,
    page * itemsPerPage.value
  );
};

const handleFilterChanged = (filters) => {
  console.log(filters);
};

const handleSearchChanged = async (query) => {
  paginatedMovies.value = movies.filter((movie) =>
    movie.title.toLocaleLowerCase().includes(query)
  );
  await nextTick();
};
</script>

<template>
  <div class="container">
    <div class="row">
      <div class="col-1">
        <div
          class="d-flex align-items-center justify-content-center position-fixed h-100vh px-4"
        >
          <Filters :movies="movies" @filter-changed="handleFilterChanged" />
        </div>
      </div>
      <div class="col-11 z-index">
        <div class="row">
          <div class="col-12">
            <div class="fs-3 px-3 my-4">Movies Query</div>
          </div>
          <div class="col-12">
            <Search @search-changed="handleSearchChanged" />
          </div>
          <div class="col-12">
            <div class="pagination-info text-muted px-2 mb-3">
              <div class="row">
                <div class="col-lg-6 col-md-6 col-sm-12">
                  <p class="d-inline-block mr-1">
                    Showing <b>{{ itemsPerPage }}</b> out of
                    <b> {{ movies.length }}</b> movies
                  </p>
                  <select
                    class="form-select-sm w-auto d-inline-block mx-lg-2 mx-sm-1"
                    aria-label="Default select example"
                    v-model="itemsPerPage"
                    @input="(evt) => handleItemsPerPageChange(evt)"
                  >
                    <option selected value="5">5</option>
                    <option value="10">10</option>
                    <option value="15">15</option>
                    <option :value="movies.length">All</option>
                  </select>
                </div>
                <div
                  class="col-lg-6 col-md-6 col-lg-6 col-sm-12 text-lg-end text-sm-center"
                >
                  <Pagination
                    :movies="movies"
                    :items-per-page="Number(itemsPerPage)"
                    @page-changed="handlePageChange"
                  />
                </div>
              </div>
            </div>
            <MovieList :movies="paginatedMovies" />
          </div>
          <div class="col-12">
            <h3>Footer</h3>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.h-100vh {
  height: 100vh;
  background: #0d161e;
  background: linear-gradient(90deg, #0d161e 30%, transparent);
  margin: auto 0;
  top: 0;
  width: 400px;
  left: 0;
}

.z-index {
  z-index: 1;
}
</style>
