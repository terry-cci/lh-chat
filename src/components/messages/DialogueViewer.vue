<script setup lang="ts">
import { ref, onMounted, computed } from "vue";
import { UserInfo } from "../menu/ChatList.vue";
import SingleMessage, { MessageInfo } from "./SingleMessage.vue";
import ScrollHint from "./ScrollHint.vue";

const props = defineProps<{
  user: UserInfo;
  messages: MessageInfo[];
  selfAvatar: string;
}>();

const container = ref<HTMLDivElement | null>(null);

const scroll = ref(NaN);
function calcScroll() {
  if (!container.value) {
    scroll.value = 0;
    return;
  }

  scroll.value =
    container.value.scrollTop /
    (container.value.scrollHeight - container.value.clientHeight);
}

function backToBottom() {
  container.value?.scrollTo(
    0,
    container.value.scrollHeight - container.value.clientHeight
  );
}

const SCROLL_HINT_BUFFER = 72;
const showScrollHint = computed(
  () =>
    container.value &&
    scroll.value !== NaN &&
    scroll.value <
      1 -
        SCROLL_HINT_BUFFER /
          (container.value.scrollHeight - container.value.clientHeight)
);

onMounted(() => {
  backToBottom();
  calcScroll();
  container.value!.style.scrollBehavior = "smooth";
});
</script>

<template>
  <div class="h-0 flex-grow relative">
    <div
      class="flex flex-col overflow-y-auto h-full p-8"
      ref="container"
      @scroll="calcScroll"
    >
      <single-message
        v-for="msg in messages"
        :key="msg.id"
        :msg="msg"
        :user="user"
        :self-avatar="selfAvatar"
      />
    </div>
    <transition name="fade">
      <scroll-hint v-if="showScrollHint" @back-to-bottom="backToBottom" />
    </transition>
  </div>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 150ms ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
