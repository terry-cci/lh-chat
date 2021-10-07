<script setup lang="ts">
import { FileInfo } from "./SingleMessage.vue";

const props = withDefaults(
  defineProps<{ file: FileInfo; download?: boolean; canDelete?: boolean }>(),
  { download: false, canDelete: false }
);

const emit = defineEmits<{ (e: "delete"): void }>();

function formatSize(size: number) {
  let i = 0;
  const units = ["B", "KB", "MB", "GB"];
  while (size >= 1024) {
    size /= 1024;
    i++;
  }
  return `${size.toFixed(2)} ${units[i]}`;
}
</script>

<template>
  <component
    :is="download ? 'button' : 'div'"
    class="
      w-full
      bg-white
      text-cyan-600
      border-2 border-cyan-700
      shadow
      rounded
      flex
      items-center
      px-2
      py-1
      transition
      relative
    "
    :class="download && ['hover:text-cyan-500', 'active:bg-gray-200']"
  >
    <svg
      xmlns="http://www.w3.org/2000/svg"
      class="h-10 w-10 mr-2"
      fill="none"
      viewBox="0 0 24 24"
      stroke="currentColor"
      v-if="download"
    >
      <path
        stroke-linecap="round"
        stroke-linejoin="round"
        stroke-width="2"
        d="M12 10v6m0 0l-3-3m3 3l3-3m2 8H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"
      />
    </svg>
    <svg
      xmlns="http://www.w3.org/2000/svg"
      class="h-10 w-10 mr-2"
      fill="none"
      viewBox="0 0 24 24"
      stroke="currentColor"
      v-else
    >
      <path
        stroke-linecap="round"
        stroke-linejoin="round"
        stroke-width="2"
        d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"
      />
    </svg>

    <div class="flex flex-col items-start">
      <span class="text-sm truncate max-w-xs text-left">
        {{ file.filename }}
      </span>
      <span class="text-xs text-gray-400">
        {{ formatSize(file.size) }}
      </span>
    </div>

    <button
      class="absolute right-1 hover:text-cyan-400 active:text-cyan-700 p-2"
      @click="emit('delete')"
      v-if="canDelete"
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
          d="M6 18L18 6M6 6l12 12"
        />
      </svg>
    </button>
  </component>
</template>
