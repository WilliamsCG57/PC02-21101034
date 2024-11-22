<template>
  <q-card class="movie-card">
    <q-card-section>
      <!-- Imagen de la película -->
      <q-img
        :src="`http://image.tmdb.org/t/p/w500${movie.poster_path}`"
        alt="Poster de {{ movie.title }}"
        style="max-height: 300px; object-fit: cover"
      />
    </q-card-section>
    <q-card-section>
      <q-card-title>{{ movie.title }}</q-card-title>
      <div class="text-caption">
        <strong>Votos:</strong> {{ movie.vote_average }} ({{
          movie.vote_count
        }})
      </div>
    </q-card-section>
  </q-card>
</template>

<style>
.movie-card {
  width: 300px;
  margin: 10px; /* Espaciado entre tarjetas */
}

.movie-card q-card-title {
  font-size: 18px;
  font-weight: bold;
  text-align: center;
}

.movie-card .text-caption {
  margin-top: 8px;
  text-align: center;
  color: #666;
}
</style>

<script>
export default {
  name: "MoviesItem",
  props: {
    movie: {
      // Recibimos una película como prop
      type: Object,
      required: true,
    },
  },
};
</script>
