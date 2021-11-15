<template>
  <div class="postcurrent">
    <form v-on:submit.prevent="updatePost()">
      <h1>Edit Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div>
        <lablel>Title:</lablel>
        <input type="text" v-model="currentPostParams.title" />
      </div>
      <div>
        <lablel>Body:</lablel>
        <input type="text" v-model="currentPostParams.body" />
      </div>
      <div>
        <lablel>Image:</lablel>
        <input type="text" v-model="currentPostParams.image" />
      </div>
      <input type="submit" value="Submit" />
    </form>
    <button v-on:click="destroyPost()">Delete</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      currentPostParams: {},
      errors: [],
    };
  },
  created: function () {
    axios.get(`/posts/${this.$route.params.id}`).then((response) => {
      console.log("Post Info:", response.data);
      this.currentPostParams = response.data;
    });
  },
  methods: {
    updatePost: function () {
      console.log("Post Updating...");

      axios
        .patch(`/posts/${this.$route.params.id}`, this.currentPostParams)
        .then((response) => {
          this.$router.push(`/posts/${response.$route.params.id}`);
        })
        .catch((error) => console.log(error.response));
    },
    destroyPost: function () {
      axios.delete(`/posts/${this.$route.params.id}`).then((response) => {
        console.log("Deleted", response.data);
        this.$router.push("/posts");
      });
    },
  },
};
</script>
