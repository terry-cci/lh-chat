<script setup lang="ts">
import { formatDate } from "../App.vue";

const now = new Date();
</script>

<template>
  <div
    class="
      bg-cyan-400
      top-0
      inset-x-0
      text-white
      h-8
      shadow
      fixed
      flex
      items-center
      justify-center
    "
  >
    <div
      class="flex items-center justify-between max-w-screen-lg px-6 flex-grow"
    >
      <button
        class="
          flex
          items-center
          transform
          border-b border-transparent
          hover:-translate-x-0.5 hover:border-white
          transition
          active:text-blue-100
        "
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-5 w-5 mr-2"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M11 19l-7-7 7-7m8 14l-7-7 7-7"
          />
        </svg>
        返回學生天地
      </button>
      <span>{{ formatDate(now) }}</span>
    </div>
  </div>
</template>
