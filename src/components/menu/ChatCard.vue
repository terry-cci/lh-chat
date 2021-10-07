<script setup lang="ts">
import { computed } from "vue";
import { UserInfo } from "./ChatList.vue";
import BaseChatCard from "./BaseChatCard.vue";
import UserAvatar from "../common/UserAvatar.vue";
import TextWithHighlight from "../common/TextWithHighlight.vue";

const props = withDefaults(
  defineProps<{ user: UserInfo; active?: boolean; query?: string }>(),
  { active: false }
);
</script>

<template>
  <base-chat-card
    class="cursor-pointer chat-card"
    :class="
      active
        ? ['bg-cyan-500', 'text-white']
        : ['bg-white', 'hover:bg-gray-100', 'text-gray-800']
    "
    :avatar-src="user.avatarSrc"
  >
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
    <h4 class="text-sm" :class="active ? ['text-gray-200'] : ['text-gray-400']">
      <text-with-highlight
        :text="user.id"
        :highlight="query || ''"
        :highlight-class="[
          active ? 'text-cyan-900' : 'text-cyan-400',
          'font-bold',
        ]"
      />
    </h4>
  </base-chat-card>
</template>
