<script setup lang="ts">
import ChatCard from "./ChatCard.vue";

export type UserInfo = {
  avatarSrc: string;
  nickname: string;
  id: string;
};

const props = defineProps<{ chats: UserInfo[]; activeChatUser?: UserInfo }>();
const emit = defineEmits<{ (e: "changeactivechat", userId: string): void }>();
</script>

<template>
  <div class="w-1/3 flex flex-col">
    <h2
      class="
        text-lg
        h-12
        flex
        items-center
        justify-center
        shadow-sm
        border-b border-cyan-200
        bg-cyan-50
        text-cyan-800
        w-full
        text-center
      "
    >
      個人通訊
    </h2>
    <div class="flex flex-col h-0 flex-grow w-full overflow-y-auto">
      <chat-card
        v-for="user in chats"
        :key="user.id"
        :user="user"
        class="border-b"
        :active="user.id === activeChatUser?.id"
        @click="emit('changeactivechat', user.id)"
      />
    </div>
  </div>
</template>
