<template>
  <div class="sort-toggle">
    <q-toggle
      v-model="value"
      label="Ordenar por popularidad"
      left-label="Fecha de lanzamiento"
      right-label="Popularidad"
      style="width: 100%"
    />
  </div>
</template>

<script>
export default {
  name: "SortToggle",
  props: {
    modelValue: {
      type: Boolean,
      default: true, // Ordenar por popularidad como predeterminado
    },
  },
  emits: ["update:modelValue"],
  computed: {
    value: {
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

<style scoped>
.sort-toggle {
  width: 100%;
}
</style>
