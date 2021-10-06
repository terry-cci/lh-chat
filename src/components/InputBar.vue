<script setup lang="ts">
import { ref, watch, computed } from "vue";
import { UserInfo } from "./ChatList.vue";
import MessageFile from "./MessageFile.vue";
import { FileInfo } from "./SingleMessage.vue";

const props = defineProps<{ user: UserInfo }>();

const inputText = ref("");
const bufferTextarea = ref<HTMLTextAreaElement | null>(null);
const inputTextarea = ref<HTMLTextAreaElement | null>(null);

const textareaLines = ref(1);

watch(inputText, (v) => {
  if (!bufferTextarea.value || !inputTextarea.value) {
    textareaLines.value = 1;
    return;
  }

  const computedStyle = window.getComputedStyle(inputTextarea.value);
  const lh =
    parseInt(computedStyle.lineHeight) || parseInt(computedStyle.fontSize);
  bufferTextarea.value.style.width = computedStyle.width;

  bufferTextarea.value.value = v;
  textareaLines.value = Math.max(
    Math.ceil(bufferTextarea.value.scrollHeight / lh),
    1
  );
});
const textareaPlaceholder = computed(
  () =>
    `向 ${
      props.user.nickname.length < 20
        ? props.user.nickname
        : props.user.nickname.substr(0, 20) + "..."
    } 發送訊息`
);

const attachmentInput = ref<HTMLInputElement | null>(null);
const attachment = ref<FileInfo | null>(null);

function onAttachmentChange() {
  if (attachmentInput.value!.files?.length) {
    attachment.value = toFileInfo(attachmentInput.value!.files[0]);
  } else attachment.value = null;
}

function toFileInfo(file: File) {
  return {
    filename: file.name,
    size: file.size,
  };
}
function deleteAttachment() {
  attachmentInput.value!.value = "";
  attachmentInput.value?.dispatchEvent(new Event("change"));
}
</script>

<template>
  <div
    class="
      w-full
      border border-cyan-400
      bg-white
      overflow-hidden
      rounded
      flex
      items-start
      flex-shrink-0
    "
  >
    <div class="flex-grow flex flex-col">
      <textarea
        type="text"
        class="px-4 absolute h-0 overflow-hidden"
        ref="bufferTextarea"
      ></textarea>

      <textarea
        type="text"
        :placeholder="textareaPlaceholder"
        class="px-4 py-2 resize-none max-h-40 overflow-hidden"
        ref="inputTextarea"
        v-model="inputText"
        :rows="textareaLines"
      ></textarea>

      <div v-if="attachment" class="p-2">
        <message-file
          :file="attachment"
          :can-delete="true"
          @delete="deleteAttachment"
        />
      </div>
    </div>

    <div class="text-cyan-500">
      <button
        class="px-2 py-2 hover:text-cyan-400 active:text-cyan-700"
        title="附加檔案"
        @click="attachmentInput!.click()"
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
            d="M15.172 7l-6.586 6.586a2 2 0 102.828 2.828l6.414-6.586a4 4 0 00-5.656-5.656l-6.415 6.585a6 6 0 108.486 8.486L20.5 13"
          />
        </svg>
      </button>
      <button
        title="發送訊息"
        class="px-2 py-2 hover:text-cyan-400 active:text-cyan-700"
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
            d="M14 5l7 7m0 0l-7 7m7-7H3"
          />
        </svg>
      </button>
    </div>

    <input
      type="file"
      id="attachment"
      class="hidden"
      ref="attachmentInput"
      @change="onAttachmentChange"
    />
  </div>
</template>
