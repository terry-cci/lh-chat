<script setup lang="ts">
import { ref, onMounted } from "vue";
import { UserInfo } from "./ChatList.vue";
import { MessageInfo } from "./SingleMessage.vue";
import DialogueViewer from "./DialogueViewer.vue";
import InputBar from "./InputBar.vue";

const props = defineProps<{
  user?: UserInfo;
  messages?: MessageInfo[];
  selfAvatar: string;
}>();
</script>

<template>
  <div class="flex-grow border-l flex h-full flex-col" v-if="user && messages">
    <dialogue-viewer
      :user="user"
      :messages="messages"
      :self-avatar="selfAvatar"
    />

    <div
      class="w-full bg-cyan-50 px-8 py-4 bg-opacity-50 flex-shrink-0 relative"
    >
      <input-bar :user="user" />
    </div>
  </div>
</template>
