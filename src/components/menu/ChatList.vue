<script setup lang="ts">
import { ref, computed, watch, nextTick } from "vue";
import ChatCard from "./ChatCard.vue";
import NewChatCard from "./NewChatCard.vue";

export type UserInfo = {
  avatarSrc?: string;
  nickname: string;
  id: string;
};

const props = defineProps<{ chats: UserInfo[]; activeChatUser?: UserInfo }>();
const emit = defineEmits<{
  (e: "changeActiveChat", userId: string): void;
  (e: "addUser", id: string): void;
}>();

const chatQuery = ref("");
const filteredChats = computed(() =>
  props.chats.filter(
    (u) =>
      !chatQuery.value ||
      u.id.includes(chatQuery.value.trim()) ||
      u.nickname.includes(chatQuery.value.trim())
  )
);

const addNewCardActive = ref(false);
const chatCardList = ref<HTMLDivElement | null>(null);
async function addUser(id: string) {
  addNewCardActive.value = false;
  emit("addUser", id);

  await nextTick();
  const i = props.chats.findIndex((u) => u.id === id);
  if (i == -1) return;
  chatCardList.value!.scrollTo(0, chatCardList.value!.children[i].offsetTop);
}
</script>

<template>
  <div class="w-1/3 flex flex-col border-r-2 border-cyan-200">
    <div class="flex flex-col shadow border-b-2 border-cyan-200">
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
          @click="addNewCardActive = true"
          id="add-user-btn"
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

      <transition name="vert-grow">
        <div
          class="border-b border-cyan-200 relative h-10 flex items-center"
          v-if="!addNewCardActive"
        >
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
      </transition>

      <transition name="vert-grow">
        <new-chat-card
          class="bg-cyan-600 h-20"
          v-if="addNewCardActive"
          @add-user="addUser"
        />
      </transition>
    </div>

    <div
      class="
        chat-card-list
        flex flex-col
        h-0
        flex-grow
        w-full
        overflow-y-auto overflow-x-hidden
        relative
      "
      ref="chatCardList"
    >
      <chat-card
        v-for="(user, i) in filteredChats"
        :key="user.id"
        :user="user"
        class="border-b"
        :active="user.id === activeChatUser?.id"
        :query="chatQuery"
        @click="emit('changeActiveChat', user.id)"
      />
    </div>
  </div>
</template>

<style scoped>
.vert-grow-enter-active,
.vert-grow-leave-active {
  transition: 150ms ease;
  transition-property: height, padding-top, padding-bottom;
  overflow: hidden;
}

.vert-grow-enter-from,
.vert-grow-leave-to {
  height: 0;
  padding-top: 0;
  padding-bottom: 0;
}

.chat-card-list {
  scroll-behavior: smooth;
}
</style>
