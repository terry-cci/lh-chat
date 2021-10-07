<script setup lang="ts">
import { ref, computed } from "vue";
import ChatCard from "./ChatCard.vue";

export type UserInfo = {
  avatarSrc: string;
  nickname: string;
  id: string;
};

const props = defineProps<{ chats: UserInfo[]; activeChatUser?: UserInfo }>();
const emit = defineEmits<{ (e: "changeactivechat", userId: string): void }>();

const chatQuery = ref("");
const filteredChats = computed(() =>
  props.chats.filter(
    (u) =>
      !chatQuery.value ||
      u.id.includes(chatQuery.value.trim()) ||
      u.nickname.includes(chatQuery.value.trim())
  )
);
</script>

<template>
  <div class="w-1/3 flex flex-col">
    <div class="flex flex-col shadow-sm">
      <div
        class="
          h-12
          flex
          items-center
          justify-center
          border-b border-cyan-200
          bg-cyan-50
          text-cyan-800
          relative
        "
      >
        <h2 class="text-lg">個人通訊</h2>
        <button
          class="
            rounded
            bg-white
            border
            p-1
            shadow-sm
            absolute
            right-2
            hover:bg-gray-50
            active:bg-gray-300
          "
          title="新增通訊對象"
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
              d="M12 4v16m8-8H4"
            />
          </svg>
        </button>
      </div>

      <div class="border-b border-cyan-200 relative h-10 flex items-center">
        <input
          type="text"
          placeholder="搜尋已有通訊..."
          class="w-full h-full px-4"
          v-model="chatQuery"
        />

        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-6 w-6 absolute right-2 text-gray-400"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
          />
        </svg>
      </div>
    </div>

    <div class="flex flex-col h-0 flex-grow w-full overflow-y-auto">
      <chat-card
        v-for="user in filteredChats"
        :key="user.id"
        :user="user"
        class="border-b"
        :active="user.id === activeChatUser?.id"
        :query="chatQuery"
        @click="emit('changeactivechat', user.id)"
      />
    </div>
  </div>
</template>
