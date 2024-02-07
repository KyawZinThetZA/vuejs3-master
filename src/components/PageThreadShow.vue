<template>
  <div class="col-large push-top">
    <h1>{{ thread.title }}</h1>

    <div class="post-list" v-for="post in thread.posts" :key="post">
      <div class="post">
        <div class="user-info">
          <a href="#" class="user-name">{{
            userById(postById(post).userId).name
          }}</a>

          <a href="#">
            <img
              class="avatar-large"
              :src="userById(postById(post).userId).avatar"
              alt=""
            />
          </a>

          <p class="desktop-only text-small">107 posts</p>
        </div>

        <div class="post-content">
          <div>
            <p>
              {{ postById(post).text }}
            </p>
          </div>
        </div>

        <div class="post-date text-faded">{{ postById(post).publishedAt }}</div>
      </div>
    </div>
  </div>
</template>

<script setup>
import sourceData from "@/data.json";
import { ref, computed } from "vue";
import { useRoute } from "vue-router";

const router = useRoute();
const threads = ref(sourceData.threads);
const posts = ref(sourceData.posts);
const users = ref(sourceData.users);
// props: {
//   id: {
//     required: true;
//     type: String;
//   }
// }

const props = defineProps({
  id: {
    required: true,
    type: String,
  },
});

const thread = computed(function name() {
  return threads.value.find((t) => t.id === this.id);
});

function postById(post) {
  return posts.value.find((p) => p.id === post);
}
function userById(user) {
  return users.value.find((u) => u.id === user);
}
</script>
