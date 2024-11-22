<template>
  <div class="vote-range-buttons">
    <h6>Filtrar por Votación</h6>
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
  name: "VoteRangeButtons",
  props: {
    selectedRange: {
      type: Object,
      default: () => ({ min: 1, max: 10 }),
    },
  },
  emits: ["update:selectedRange"],
  data() {
    return {
      ranges: [
        { label: "1-3", min: 1, max: 3.99 },
        { label: "4-6", min: 4, max: 6.99 },
        { label: "7-10", min: 7, max: 10 },
        { label: "Todas", min: 1, max: 10 },
      ],
    };
  },
  methods: {
    filterByRange(range) {
      this.$emit("update:selectedRange", range); // Emitir el rango seleccionado
    },
  },
};
</script>

<style scoped>
.vote-range-buttons {
  display: flex;
  gap: 5px;
  flex-wrap: wrap;
}
</style>
