<script setup lang="ts">
import { provide, ref } from "vue";
import { Tweet } from "@/types/tweet";
import { userNameKey } from "./../key/user";
import TweetFormComponent from "./TweetForm.vue";
import TweetList from "./TweetList.vue";
import UserModal from "./UserModal.vue";

const tweets = ref<Tweet[]>([
  {
    id: "1",
    description: "Hello!",
  },
  {
    id: "2",
    description: "Example",
  },
]);

const onSubmit = (description: string) => {
  tweets.value = [
    ...tweets.value,
    {
      id: Math.random().toString(),
      description,
    },
  ];
};

const onDelete = (id: string) => {
  console.log(`id=${id} is deleted;`);
  tweets.value = tweets.value.filter((tweet) => tweet.id !== id);
};

const isOpenModal = ref<boolean>(false);
const userName = ref<string>("");
const closeUserModal = (username:string) => {
  isOpenModal.value = false;
  userName.value = username;
};

provide(userNameKey, userName);
</script>

<template>
  <div class="setting">
    <button @click="isOpenModal = !isOpenModal">Settings</button>
  </div>
  <Teleport to="body">
    <UserModal :show="isOpenModal" @close="closeUserModal" />
  </Teleport>
  <h1>Twitter</h1>
  <TweetFormComponent @submit="onSubmit" :show="isOpenModal" />
  <TweetList :tweets="tweets" @onDelete="onDelete" />
</template>

<style scoped>
.setting {
  display: flex;
  flex-direction: column;
  font-size: 1.5rem;
  font-weight: bold;
  position: absolute;
  top: 20px;
  right: 20px;
}
</style>
