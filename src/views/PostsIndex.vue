<template>
  <div class="postindex">
    <h1>{{ message }}</h1>
    <div v-for="post in posts" :key="post.id">
      <router-link v-bind:to="`/posts/${post.id}`">
        <h2>{{ post.title }}</h2>
      </router-link>
      <img :src="post.image_url" :alt="post.title" />
      <p>{{ post.body }}</p>
    </div>
  </div>
</template>
;
<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Posts:",
      posts: [],
    };
  },
  created: function () {
    this.indexPosts();
  },
  methods: {
    indexPosts: function () {
      axios.get("http://localhost:3000/posts").then((response) => {
        console.log("Posts", response.data);
        this.posts = response.data;
      });
    },
  },
};
</script>
;
