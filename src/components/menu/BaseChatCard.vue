<script setup lang="ts">
import UserAvatar from "../common/UserAvatar.vue";
const props = defineProps<{ avatarSrc?: string }>();
</script>

<template>
  <div class="flex items-center px-6 py-2 w-full">
    <user-avatar :image-src="avatarSrc" class="w-14 h-14 flex-shrink-0">
      <template #default v-if="$slots.avatar">
        <slot name="avatar" />
      </template>
    </user-avatar>
    <div class="ml-4 flex flex-col w-0 flex-grow">
      <slot />
    </div>
  </div>
</template>
