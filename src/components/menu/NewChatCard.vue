<script setup lang="ts">
import { ref, onMounted } from "vue";
import BaseChatCard from "./BaseChatCard.vue";

const emit = defineEmits<{ (e: "addUser", id: string): void }>();

const userId = ref("");
const userIdInput = ref<HTMLInputElement | null>(null);
const confirmed = ref(false);

function addUser() {
  if (confirmed.value) return;

  confirmed.value = true;
  emit("addUser", userId.value);
}

function onBlur(e: FocusEvent) {
  const relatedTarget = e.relatedTarget as HTMLElement;
  if (relatedTarget?.id === "add-user-btn") {
    userIdInput.value!.focus();
    return;
  }

  addUser();
}

onMounted(() => {
  userIdInput.value!.focus();
});
</script>

<template>
  <base-chat-card>
    <template #default>
      <h3 class="text-white">新增個人通訊</h3>
      <input
        type="text"
        placeholder="請輸入通訊對象的編號..."
        class="
          text-sm
          bg-transparent
          placeholder-gray-300
          text-white
          border-b border-white
          w-full
          focus:outline-none
        "
        @blur="onBlur"
        @keydown.enter="addUser"
        v-model="userId"
        ref="userIdInput"
      />
    </template>
  </base-chat-card>
</template>
