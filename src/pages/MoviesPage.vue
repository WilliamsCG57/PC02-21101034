<template>
  <div class="movies-page q-ml-md q-mr-xl">
    <!-- Componente para el filtro de búsqueda -->
    <div class="movies-filter q-ml-md q-mr-xl">
      <MoviesFilter v-model="query" />
    </div>

    <!-- Componente para el filtro de rango de votación -->
    <div class="vote-range-filter q-ml-md q-mr-xl">
      <VoteRangeButtons v-model:selectedRange="voteRange" />
    </div>

    <!-- Componente para el filtro de conteo de votos -->
    <div class="vote-count-filter q-ml-md q-mr-xl">
      <VoteCountRangeButtons v-model:selectedCountRange="voteCountRange" />
    </div>

    <!-- Componente de ordenamiento -->
    <div class="sort-toggle-filter q-ml-md q-mr-xl">
      <SortToggle v-model="isPopular" />
    </div>

    <!-- Componente de filtro por año de lanzamiento -->
    <div class="release-year-filter q-ml-md q-mr-xl">
      <ReleaseYearFilter v-model="releaseYear" />
    </div>

    <!-- Botón para aplicar filtros -->
    <div class="q-mt-sm q-ml-md q-mr-xl">
      <q-btn
        label="Buscar"
        color="primary"
        @click="fetchMovies"
        style="width: 100%"
      />
    </div>

    <!-- Botón para borrar filtros -->
    <div class="q-mt-sm q-ml-md q-mr-xl">
      <q-btn
        label="Borrar filtros"
        color="negative"
        @click="clearFilters"
        style="width: 100%"
      />
    </div>

    <!-- Lista de películas -->
    <div class="movies-list">
      <MoviesList :movies="filteredMovies" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import MoviesFilter from "src/components/movies/MoviesFilter.vue";
import VoteRangeButtons from "src/components/movies/VoteRangeButtons.vue";
import VoteCountRangeButtons from "src/components/movies/VoteCountRangeButtons.vue";
import SortToggle from "src/components/movies/SortToggle.vue";
import ReleaseYearFilter from "src/components/movies/ReleaseYearFilter.vue";
import MoviesList from "src/components/movies/MoviesList.vue";

export default {
  name: "MoviesPage",
  components: {
    MoviesFilter,
    VoteRangeButtons,
    VoteCountRangeButtons,
    SortToggle,
    ReleaseYearFilter,
    MoviesList,
  },
  data() {
    return {
      query: "",
      voteRange: { min: 1, max: 10 },
      voteCountRange: { min: 0, max: 6000 },
      isPopular: true,
      releaseYear: null,
      movies: [],
      currentPage: 1, // Añadimos una propiedad para controlar la página
    };
  },
  computed: {
    filteredMovies() {
      return this.movies.filter((movie) => {
        return (
          movie.title.toLowerCase().includes(this.query.toLowerCase()) &&
          movie.vote_average >= this.voteRange.min &&
          movie.vote_average <= this.voteRange.max &&
          movie.vote_count >= this.voteCountRange.min &&
          movie.vote_count <= this.voteCountRange.max
        );
      });
    },
  },
  methods: {
    // Este método realiza la carga de películas
    async fetchMovies() {
      const sortBy = this.isPopular ? "popularity.desc" : "release_date.desc";

      try {
        const response = await axios.get(
          "https://api.themoviedb.org/3/discover/movie",
          {
            headers: {
              Authorization:
                "Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiJhMzJlZjM0NThmOTdlNzY4NDViNzA0MjNmZmVkN2I5YyIsIm5iZiI6MTczMjA1NjgzMy4yMTI3MTAxLCJzdWIiOiI2NzNjZmRlZTRkNmRiMDBkOTNkNGRmOTciLCJzY29wZXMiOlsiYXBpX3JlYWQiXSwidmVyc2lvbiI6MX0.5NeNTeMIFHqZ6d60ZZyZQQDGq1wRb-io9CSzxClz9NQ",
            },
            params: {
              language: "es-PE",
              sort_by: sortBy,
              primary_release_year: this.releaseYear || undefined,
              page: this.currentPage, // Agregamos la propiedad de página
            },
          }
        );
        this.movies = response.data.results || [];
      } catch (error) {
        console.error("Error al obtener películas:", error);
      }
    },

    // Método para borrar todos los filtros
    clearFilters() {
      this.query = ""; // Limpiamos el buscador
      this.voteRange = { min: 1, max: 10 }; // Restablecemos el rango de votos
      this.voteCountRange = { min: 0, max: 6000 }; // Restablecemos el rango de conteo de votos
      this.isPopular = true; // Restablecemos el orden de popularidad
      this.releaseYear = null; // Restablecemos el año de lanzamiento
      this.currentPage = 1; // Restablecemos la página a la inicial

      this.fetchMovies(); // Volvemos a cargar las películas con los filtros por defecto
    },
  },
  mounted() {
    this.fetchMovies(); // Llamamos fetchMovies al inicio
  },
};
</script>

<style>
.movies-page {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.movies-filter,
.vote-range-filter,
.sort-toggle-filter,
.release-year-filter {
  width: 25%;
}

.vote-count-filter {
  display: flex;
  flex-wrap: nowrap;
  gap: 0.5rem;
}
</style>
