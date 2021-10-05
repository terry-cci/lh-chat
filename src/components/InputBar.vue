<script setup lang="ts">
import { ref, watch } from "vue";
import { UserInfo } from "./ChatList.vue";

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
</script>

<template>
  <div
    class="
      w-full
      border border-cyan-400
      overflow-hidden
      rounded
      flex
      items-end
      flex-shrink-0
    "
  >
    <textarea
      type="text"
      class="px-4 absolute h-0 overflow-hidden"
      ref="bufferTextarea"
    ></textarea>
    <textarea
      type="text"
      :placeholder="`向 ${
        user.nickname.length < 20
          ? user.nickname
          : user.nickname.substr(0, 20) + '...'
      } 發送訊息`"
      class="px-4 py-2 flex-grow resize-none max-h-40 overflow-hidden"
      ref="inputTextarea"
      v-model="inputText"
      :rows="textareaLines"
    ></textarea>
    <button
      class="text-cyan-500 px-3 py-2 hover:text-cyan-400 active:text-cyan-700"
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
</template>
