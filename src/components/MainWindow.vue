<script lang="ts">
const users: UserInfo[] = [
  {
    avatarSrc: "https://www.louhau.edu.mo/estar/system/images/face/f37.gif",
    nickname: "上網的小明",
    id: "123456",
  },
  {
    avatarSrc: "https://www.louhau.edu.mo/estar/system/images/face/f05.gif",
    nickname: "鍾文銘",
    id: "012345",
  },
  {
    avatarSrc: "https://www.louhau.edu.mo/estar/system/images/face/f26.gif",
    nickname: "Deja vu",
    id: "171022",
  },
  {
    avatarSrc: "https://www.louhau.edu.mo/estar/system/images/face/f13.gif",
    nickname: "李老師",
    id: "02123",
  },
  {
    avatarSrc: "https://www.louhau.edu.mo/estar/system/images/face/f15.gif",
    nickname: "Annies",
    id: "99345",
  },
  {
    avatarSrc: "https://www.louhau.edu.mo/estar/system/images/face/f45.gif",
    nickname: "Ipsul CC.",
    id: "203069",
  },
  {
    avatarSrc: "https://www.louhau.edu.mo/estar/system/images/face/f17.gif",
    nickname: "asdugqoweiyrgoydgodfybqeoiygbaofygwqoerygowreygqewoy",
    id: "071366",
  },
  {
    avatarSrc: "https://www.louhau.edu.mo/estar/system/images/face/f02.gif",
    nickname: "Err",
    id: "081087",
  },
  {
    avatarSrc: "https://www.louhau.edu.mo/estar/system/images/face/f32.gif",
    nickname: "莫聽穿林打葉聲何妨吟嘯且徐行竹杖芒鞋輕勝馬誰怕一簑煙雨任平生",
    id: "071212",
  },
  {
    avatarSrc: "https://www.louhau.edu.mo/estar/system/images/face/f31.gif",
    nickname: "whatever",
    id: "123501",
  },
  {
    avatarSrc: "https://www.louhau.edu.mo/estar/system/images/face/f30.gif",
    nickname: "火炎焱燚",
    id: "051055",
  },
  {
    avatarSrc: "https://www.louhau.edu.mo/estar/system/images/face/f41.gif",
    nickname: "안녕하세요",
    id: "991022",
  },
];

const msgs: MessageInfo[] = [
  {
    id: 1,
    content: "Hello world!",
    type: MessageType.Received,
    sentAt: new Date("2021-10-03"),
    fromIP: "192.168.0.4",
  },
  {
    id: 2,
    content: "不盡長江滾滾流~",
    type: MessageType.Sent,
    sentAt: new Date("2021-10-03 09:00"),
    fromIP: "192.168.0.4",
  },
  {
    id: 3,
    content:
      "qe3uhrpuhpwoqrhpuohasdofnpqwuehrpowuehrpqwuhqwerpuhdaspfuhqweroduhfuqhweorhodiauhfoiwqepdsfhpqewoihrpqowierhpqwherposidnvobapwuhoruhwr",
    type: MessageType.Received,
    sentAt: new Date("2021-10-03 09:21"),
    fromIP: "192.168.0.4",
  },
  {
    id: 4,
    content: "WTF",
    type: MessageType.Received,
    sentAt: new Date("2021-10-03 09:22"),
    fromIP: "192.168.0.4",
  },
  {
    id: 5,
    content: "啊這",
    type: MessageType.Received,
    sentAt: new Date("2021-10-03 10:00"),
    fromIP: "192.168.0.4",
  },
  {
    id: 6,
    content: "强譴",
    type: MessageType.Sent,
    sentAt: new Date("2021-10-04 14:13"),
    fromIP: "192.168.0.4",
  },
  {
    id: 7,
    content: "Errrr",
    type: MessageType.Sent,
    sentAt: new Date("2021-10-04 14:13"),
    fromIP: "192.168.0.4",
  },
  {
    id: 8,
    content: "各位同學,現附科技名人及一部份練習,請大家抽空温習!\n陳秀珠老師",
    type: MessageType.Received,
    sentAt: new Date("2021-10-05 00:00"),
    fromIP: "192.168.0.4",
    attachment: {
      filename: "歴史選擇題_2.html",
      size: 67584,
    },
  },
  {
    id: 8,
    content:
      "各位高一、高二及高三級同學：\n寄上300題外交知識賽資料，以供複習。\n                       公民科組",
    type: MessageType.Sent,
    sentAt: new Date("2021-10-05 09:18"),
    attachment: {
      filename: "-第十二屆2021年--外交知識競賽預習題目.pdf",
      size: 1071104,
    },
    fromIP: "192.168.0.4",
  },
  {
    id: 9,
    content:
      "呼籲市民堅持戴口罩 衛生局：現時不適宜放鬆\n\n早前因應本地疫情逐趨平穩，當局曾考慮調整戴口罩指引,但最近香港、北京等本來疫情控制較好的地方，重新出現源頭未明的新冠肺炎感染個案，而且短時間傳播，衛生局認為戴口罩仍是一個很重要的防疫措施，現時不適宜放鬆。傳染病防制暨疾病監測部協調員梁亦好（圓圖）醫生昨日回應電台時事節目「澳門講場」聽眾表示，當局曾研究修改本澳戴口罩指引，能否在一些情況下容許不戴口罩，但最近尤其以北京的情況，數日出現多宗確診病例。\n\n梁亦好稱，明白近日天氣炎熱，市民戴口罩十分不便，雖然本澳多日沒有確診，但當局不敢肯定社區沒有無狀況感染者，甚至輸入本澳的物品是否存在病毒可令人感染，都要關注。她表示，全民戴口罩的其他地方都顯示較有效控制疫情，因此當局認為短時間內，本澳戴口罩的指引不能放鬆，並要更嚴謹。",
    type: MessageType.Received,
    sentAt: new Date(),
    fromIP: "192.168.0.4",
  },
];
</script>

<script setup lang="ts">
import { ref, computed } from "vue";
import ChatList, { UserInfo } from "./ChatList.vue";
import MessagePanel from "./MessagePanel.vue";
import { MessageInfo, MessageType } from "./SingleMessage.vue";

const chatUsers = ref(users);

const selfAvatarSrc = ref(
  "https://www.louhau.edu.mo/estar/system/images/face/f17.gif"
);
const activeChatUserId = ref("171022");
const activeChatUser = computed(() =>
  chatUsers.value.find((u) => u.id === activeChatUserId.value)
);

function changeChat(userId: string) {
  activeChatUserId.value = userId;
}

const activeMessages = ref(msgs);
</script>

<template>
  <div
    class="
      w-full
      h-5/6
      max-w-screen-lg
      bg-white
      border-2 border-cyan-200
      overflow-hidden
      shadow
      rounded
      flex
    "
  >
    <chat-list
      :chats="chatUsers"
      :active-chat-user="activeChatUser"
      @changeactivechat="changeChat"
    />
    <message-panel
      :user="activeChatUser"
      :messages="activeMessages"
      :self-avatar="selfAvatarSrc"
    />
  </div>
</template>
