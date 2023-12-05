<script lang="ts" setup>
import { ref } from "vue";
import FullCalendar from "@fullcalendar/vue3";
import dayGridPlugin from "@fullcalendar/daygrid";
import timeGridPlugin from "@fullcalendar/timegrid";

const currentView = ref("dayGridMonth"); // 初期表示を月表示に設定

const calendarOptions = ref({
  plugins: [dayGridPlugin, timeGridPlugin],
  initialView: currentView.value,
  // 他のカレンダーオプションをここに追加
});

// 表示モードを設定する関数
const setCurrentView = (view: any) => {
  currentView.value = view;
};
</script>

<template>
  <div>
    <button @click="setCurrentView('dayGridMonth')">月表示</button>
    <button @click="setCurrentView('timeGridWeek')">週表示</button>
    <FullCalendar :options="calendarOptions" />
  </div>
</template>
