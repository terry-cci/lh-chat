<script setup lang="ts">
import { computed } from "vue";
import { UserInfo } from "./ChatList.vue";
import UserAvatar from "./UserAvatar.vue";
import TextWithHighlight from "./TextWithHighlight.vue";

const props = withDefaults(
  defineProps<{ user: UserInfo; active?: boolean; query?: string }>(),
  { active: false }
);
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
      <h3 class="w-48 truncate">
        <text-with-highlight
          :text="user.nickname"
          :highlight="query || ''"
          :highlight-class="[
            active ? 'text-cyan-900' : 'text-cyan-400',
            'font-bold',
          ]"
        />
      </h3>
      <h4
        class="text-sm"
        :class="active ? ['text-gray-200'] : ['text-gray-400']"
      >
        <text-with-highlight
          :text="user.id"
          :highlight="query || ''"
          :highlight-class="[
            active ? 'text-cyan-900' : 'text-cyan-400',
            'font-bold',
          ]"
        />
      </h4>
    </div>
  </div>
</template>
