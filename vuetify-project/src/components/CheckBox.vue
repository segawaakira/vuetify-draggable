<template>
  <v-checkbox :hide-details="true" v-model="isChecked" />
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";

export default defineComponent({
  props: {
    modelValue: {
      type: Boolean,
      required: true,
    },
  },
  computed: {
    isChecked: {
      get() {
        return this.modelValue;
      },
      set(value) {
        this.$emit("update:modelValue", value);
      },
    },
  },
});
</script>
