<script setup lang="ts">
import { Tweet } from "@/types/tweet";
import TweetComponent from "./Tweet.vue";
import { defineEmits } from "vue";

const props = defineProps<{
  tweets: Tweet[];
}>();

const emits = defineEmits<{
  (e: "onDelete", id: string):void
}>();

const onDelete = (id: string) => {
  emits("onDelete", id)
};
</script>

<template>
  <div>
    <ul>
      <li v-for="tweet in props.tweets">
        <TweetComponent :tweet="tweet" @delete="onDelete" />
      </li>
    </ul>
  </div>
</template>

<style scoped>
ul {
  list-style: none;
  padding: 0;
  height: 400px;
}

li {
  margin-top: 1rem;
}
</style>
