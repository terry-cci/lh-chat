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

function formatSize(size: number) {
  let i = 0;
  const units = ["B", "KB", "MB", "GB"];
  while (size >= 1024) {
    size /= 1024;
    i++;
  }
  return `${size.toFixed(2)} ${units[i]}`;
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
      class="mt-2 flex flex-col"
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
        <button
          v-if="msg.attachment"
          class="
            w-full
            bg-white
            text-cyan-600
            border-2 border-cyan-700
            shadow
            rounded
            mt-4
            mb-1
            flex
            items-center
            px-2
            py-1
            transition
            hover:text-cyan-500
            active:bg-gray-200
          "
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-10 w-10 mr-2"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M12 10v6m0 0l-3-3m3 3l3-3m2 8H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"
            />
          </svg>

          <div class="flex flex-col items-start">
            <span class="text-sm truncate max-w-xs text-left">
              {{ msg.attachment.filename }}
            </span>
            <span class="text-xs text-gray-400">
              {{ formatSize(msg.attachment.size) }}
            </span>
          </div>
        </button>
      </div>

      <span>
        <span class="text-xs text-cyan-500">{{ formatTime(msg.sentAt) }}</span>
        <span class="text-xs text-gray-500"> ({{ msg.fromIP }})</span>
      </span>
    </div>
  </div>
</template>
