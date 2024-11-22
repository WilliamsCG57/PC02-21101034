<template>
  <div class="release-year-filter">
    <q-input
      v-model="value"
      label="Año de lanzamiento"
      type="number"
      min="1900"
      max="2024"
      outlined
      dense
      style="width: 100%"
    />
  </div>
</template>

<script>
export default {
  name: "ReleaseYearFilter",
  props: {
    modelValue: {
      type: Number,
      default: null,
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
.release-year-filter {
  width: 100%;
}
</style>
