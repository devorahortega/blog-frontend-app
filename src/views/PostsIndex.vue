<template>
  <div class="postindex">
    <h1>{{ message }}</h1>
    <div>
      Search by title:
      <input type="text" v-model="titleFilter" list="titles" />
      <datalist id="titles">
        <option v-for="post in posts" :key="post.id">{{ recipe.title }}</option>
      </datalist>
    </div>

    <div>
      <button v-on:click="setSortAttribute('title')">Sort by Title</button>
    </div>

    <div v-for="post in posts" :key="post.id">
      <div
        v-for="post in posts"
        v-on:click="currentPost = post"
        v-bind:class="{ selected: post === currentPost }"
        :key="post.id"
      >
        <router-link v-bind:to="`/posts/${post.id}`">
          <h2>{{ post.title }}</h2>
        </router-link>
        <img :src="post.image_url" :alt="post.title" />
        <p>{{ post.body }}</p>
        <p class="date">Created: {{ dateCreated(post.created_at) }}</p>
      </div>
    </div>
  </div>
</template>
;
<style>
.selected {
  background-color: black;
  transition: background-color 2s ease;
}
</style>

<script>
import axios from "axios";
import moment from "moment";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      message: "Posts:",
      posts: [],
      currentPost: {},
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

    dateCreated: function (date) {
      return moment(date).format("dddd, MMMM Do YYYY, h:mm:ss a");
    },
  },
};
</script>
;
