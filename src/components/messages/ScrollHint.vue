<script setup lang="ts">
const emit = defineEmits<{ (e: "backToBottom"): void }>();
</script>

<template>
  <div>
    <div
      class="
        absolute
        bottom-0
        inset-x-0
        bg-gradient-to-t
        h-8
        text-cyan-500
        from-white
        to-transparent
        pointer-events-none
      "
    ></div>
    <button
      class="
        absolute
        bottom-8
        left-1/2
        bg-white
        rounded
        border border-gray-400
        shadow
        transform
        -translate-x-1/2
        p-1
        text-cyan-500
        transition
        hover:translate-y-0.5
      "
      @click="emit('backToBottom')"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-6 w-6"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M19 13l-7 7-7-7m14-8l-7 7-7-7"
        />
      </svg>
    </button>
  </div>
</template>
