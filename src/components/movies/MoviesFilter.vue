<template>
  <div class="movie-search-filter">
    <q-input
      v-model="searchQuery"
      label="Buscar película"
      debounce="300 "
      outlined
      dense
      style="width: 100%"
    />
  </div>
</template>

<style scoped>
.movie-search-filter {
  margin-bottom: 20px;
  max-width: 800px;
  margin: 0 auto;
  margin-top: 20px;
}

q-input {
  width: 100%;
  max-width: 300px;
}
</style>

<script>
export default {
  name: "MoviesFilter",
  props: {
    modelValue: {
      type: String,
      default: "",
    },
  },
  computed: {
    searchQuery: {
      get() {
        return this.modelValue;
      },
      set(value) {
        this.$emit("update:modelValue", value);
      },
    },
  },
};
</script>
