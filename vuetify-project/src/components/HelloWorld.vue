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
    <hr />

    <div class="d-flex justify-space-around">
      <v-btn>
        Start
        <v-tooltip activator="parent" location="start">Tooltip</v-tooltip>
      </v-btn>

      <v-btn>
        End
        <v-tooltip activator="parent" location="end">Tooltip</v-tooltip>
      </v-btn>

      <v-btn>
        Top
        <v-tooltip activator="parent" location="top"
          ><span>2023/10/07(土) - 2023/10/09(月)</span></v-tooltip
        >
      </v-btn>

      <v-btn>
        Bottom
        <v-tooltip activator="parent" location="bottom">Tooltip</v-tooltip>
      </v-btn>
    </div>

    <div>
      <v-date-picker
        class="date-picker-container"
        max-width="100%"
        height="auto"
        locale="ja"
      />
    </div>
    <div>
      <v-date-picker-month
        class="date-picker-container"
        max-width="100%"
        height="auto"
        locale="ja"
      />
    </div>
    {{ date }}
    <div>
      <Datepicker :inline="true" locale="jp" v-model="date" autoApply />
    </div>
    <div>
      <Datepicker monthPicker :inline="true" locale="jp" />
    </div>
  </v-container>
</template>

<script lang="ts" setup>
//
import { VueDraggableNext } from "vue-draggable-next";
import { ref } from "vue";
import Checkbox from "./Checkbox.vue";
import Datepicker from "@vuepic/vue-datepicker";
import "@vuepic/vue-datepicker/dist/main.css";
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
const date = ref(new Date());
</script>
