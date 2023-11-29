<template>
  <v-container class="fill-height">
    <VueDraggableNext
      v-model="items"
      :move="onMove"
      filter=".is-disabled"
      ghost-class="dragging-item"
      handle=".drag-indicator-container"
    >
      <div v-for="item in items" :key="item.name">
        <span class="drag-indicator-container"> drag </span>
        <span> {{ item.name }} </span>
        <!-- <v-checkbox :hide-details="true" v-model="item.isChecked" /> -->
        <Checkbox
          :modelValue="item.isChecked"
          @update:modelValue="(val) => (item.isChecked = val)"
        />
      </div>
    </VueDraggableNext>
    <pre>
      {{ items }}
    </pre>
  </v-container>
</template>

<script lang="ts" setup>
//
import { VueDraggableNext } from "vue-draggable-next";
import { ref } from "vue";
import Checkbox from "./Checkbox.vue";
const items = ref([
  {
    name: "Item 1",
    isChecked: true,
  },
  {
    name: "Item 2",
    isChecked: false,
  },
]);

const onMove = ({ relatedContext, draggedContext }: any) => {
  const relatedElement = relatedContext.element;
  const draggedElement = draggedContext.element;
  return (
    (!relatedElement || !relatedElement.isDisabled) &&
    !draggedElement.isDisabled
  );
};
</script>
