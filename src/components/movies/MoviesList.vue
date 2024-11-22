<template>
  <h6>Listado de Películas</h6>
  <div class="movies-list">
    <div class="movies-grid">
      <div class="movie-item" v-for="movie in movies" :key="movie.id">
        <MoviesItem :movie="movie" />
      </div>
    </div>
  </div>
</template>

<style>
.movies-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 20px;
}
</style>

<script>
import MoviesItem from "src/components/movies/MoviesItem.vue";

export default {
  name: "MoviesList",
  props: {
    movies: {
      type: Array,
      required: true,
    },
  },
  components: { MoviesItem },
};
</script>
