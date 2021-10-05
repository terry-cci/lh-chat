<script setup lang="ts">
import { computed } from "vue";
import { UserInfo } from "./ChatList.vue";
import UserAvatar from "./UserAvatar.vue";

const props = withDefaults(
  defineProps<{ user: UserInfo; active?: boolean }>(),
  { active: false }
);
const avatarImageCss = computed(() => `url(${props.user.avatarSrc})`);
</script>

<template>
  <div
    class="flex items-center px-6 py-2 w-full cursor-pointer"
    :class="
      active
        ? ['bg-cyan-500', 'text-white']
        : ['bg-white', 'hover:bg-gray-100', 'text-gray-800']
    "
  >
    <user-avatar :image-src="user.avatarSrc" class="w-14 h-14" />
    <div class="ml-4 flex flex-col">
      <h3 class="w-48 truncate">{{ user.nickname }}</h3>
      <h4
        class="text-sm"
        :class="active ? ['text-gray-200'] : ['text-gray-400']"
      >
        {{ user.id }}
      </h4>
    </div>
  </div>
</template>
