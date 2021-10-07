<script setup lang="ts">
import { computed } from "vue";

const props = defineProps<{
  imageSrc: string;
}>();
const imageCss = computed(() => `url(${props.imageSrc})`);
</script>

<template>
  <div
    class="user-avatar rounded border shadow-inner flex-shrink-0 bg-cyan-50"
  ></div>
</template>

<style scoped>
.user-avatar {
  background-image: v-bind("imageCss");
  background-size: cover;
  background-position: 50% 20%;
}
</style>
