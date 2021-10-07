<script setup lang="ts">
import { computed } from "vue";

const props = defineProps<{
  imageSrc?: string;
}>();
const imageCss = computed(() => props.imageSrc && `url(${props.imageSrc})`);
</script>

<template>
  <div
    class="
      user-avatar
      rounded
      border
      shadow-inner
      flex-shrink-0
      bg-cyan-50
      flex
      items-center
      justify-center
    "
  >
    <slot />

    <svg
      xmlns="http://www.w3.org/2000/svg"
      class="w-3/4 text-cyan-500"
      fill="none"
      viewBox="0 0 24 24"
      stroke="currentColor"
      v-if="!$slots.default && !imageSrc"
    >
      <path
        stroke-linecap="round"
        stroke-linejoin="round"
        stroke-width="2"
        d="M8.228 9c.549-1.165 2.03-2 3.772-2 2.21 0 4 1.343 4 3 0 1.4-1.278 2.575-3.006 2.907-.542.104-.994.54-.994 1.093m0 3h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
      />
    </svg>
  </div>
</template>

<style scoped>
.user-avatar {
  background-image: v-bind("imageCss");
  background-size: cover;
  background-position: 50% 20%;
}
</style>
