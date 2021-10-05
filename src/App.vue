<script lang="ts">
export function getChineseNumber(number: number) {
  return ["零", "一", "二", "三", "四", "五", "六", "七"][number];
}

export function formatDate(date: Date) {
  return `${date.getFullYear()}年${
    date.getMonth() + 1
  }月${date.getDate()}日 (星期${
    date.getDay() == 0 ? "日" : getChineseNumber(date.getDay())
  })`;
}
</script>

<script setup lang="ts">
import TheHeader from "./components/TheHeader.vue";
import MainWindow from "./components/MainWindow.vue";
</script>

<template>
  <div
    class="w-full h-full flex flex-col items-center justify-center bg-gray-100"
  >
    <the-header />
    <main-window />
  </div>
</template>
