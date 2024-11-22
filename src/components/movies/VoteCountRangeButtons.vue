<template>
  <div class="vote-count-range-buttons">
    <h6>Filtrar por Conteo de Votos</h6>
    <q-btn
      v-for="(range, index) in ranges"
      :key="index"
      :label="range.label"
      flat
      color="primary"
      @click="filterByRange(range)"
    />
  </div>
</template>

<script>
export default {
  name: "VoteCountRangeButtons",
  props: {
    selectedCountRange: {
      type: Object,
      default: () => ({ min: 0, max: 6000 }),
    },
  },
  emits: ["update:selectedCountRange"],
  data() {
    return {
      ranges: [
        { label: "0-1000", min: 0, max: 1000 },
        { label: "1001-3000", min: 1001, max: 3000 },
        { label: "3001-6000", min: 3001, max: 6000 },
        { label: "Todos", min: 0, max: 6000 },
      ],
    };
  },
  methods: {
    filterByRange(range) {
      this.$emit("update:selectedCountRange", range); // Emitir el rango seleccionado
    },
  },
};
</script>

<style scoped>
.vote-count-range-buttons {
  display: flex;
  gap: 0px;
  flex-wrap: wrap;
}
</style>
