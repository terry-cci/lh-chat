<script lang="ts">
export enum MessageType {
  Received,
  Sent,
}

export type FileInfo = {
  filename: string;
  size: number;
};

export type MessageInfo = {
  id: number;
  content: string;
  type: MessageType;
  sentAt: Date;
  fromIP: string;
  attachment?: FileInfo;
};
</script>

<script setup lang="ts">
import { computed } from "vue";
import { UserInfo } from "./ChatList.vue";
import UserAvatar from "./UserAvatar.vue";
import MessageFile from "./MessageFile.vue";
const props =
  defineProps<{ msg: MessageInfo; user: UserInfo; selfAvatar: string }>();

const isSentMessage = computed(() => props.msg.type === MessageType.Sent);

function formatTime(time: Date) {
  return `${time.getFullYear()}-${(time.getMonth() + 1)
    .toString()
    .padStart(2, "0")}-${time.getDate().toString().padStart(2, "0")} ${time
    .getHours()
    .toString()
    .padStart(2, "0")}:${time.getMinutes().toString().padStart(2, "0")}`;
}
</script>

<template>
  <div
    class="flex w-full items-start"
    :class="isSentMessage ? ['justify-end'] : ['justify-start']"
  >
    <user-avatar
      :image-src="isSentMessage ? selfAvatar : user.avatarSrc"
      class="w-10 h-10 border-cyan-400"
      :class="isSentMessage ? ['order-2', 'ml-1.5'] : ['mr-1.5']"
    />

    <div
      class="mt-2 flex flex-col group"
      :class="isSentMessage ? ['items-end'] : ['items-start']"
    >
      <div
        class="
          rounded-xl
          border border-cyan-500
          px-3
          py-1
          shadow
          max-w-md
          break-all
          whitespace-pre-wrap
        "
        :class="
          isSentMessage
            ? ['rounded-tr-none', ' bg-cyan-400', 'text-white']
            : ['rounded-tl-none', 'bg-white', 'text-cyan-900']
        "
      >
        <span>
          {{ msg.content }}
        </span>
        <message-file
          v-if="msg.attachment"
          :file="msg.attachment"
          :download="true"
          class="mt-4 mb-1"
        />
      </div>

      <span
        class="
          date-info
          opacity-0
          h-0
          transition
          duration-500
          group-hover:opacity-100
          flex
        "
      >
        <span class="text-xs text-cyan-500">{{ formatTime(msg.sentAt) }}</span>
        <span class="text-xs text-gray-500"> ({{ msg.fromIP }})</span>
      </span>
    </div>
  </div>
</template>

<style scoped>
.date-info {
  transition-property: opacity, height;
}
.group:hover .date-info {
  height: 1em;
}
</style>
