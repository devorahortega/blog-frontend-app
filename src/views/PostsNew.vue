<template>
  <div class="postnew">
    <form v-on:submit.prevent="createPost()">
      <h1>{{ message }}</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div>
        <lablel>Title:</lablel>
        <input type="text" v-model="newPostParams.title" />
      </div>
      <div>
        <lablel>Body:</lablel>
        <input type="text" v-model="newPostParams.body" />
      </div>
      <div>
        <lablel>Image:</lablel>
        <input type="text" v-model="newPostParams.image" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Create a Post:",
      newPostParams: {},
      errors: [],
    };
  },
  methods: {
    createPost: function () {
      axios
        .post("/posts", this.newPostParams)
        .then(() => {
          this.$router.push("/posts");
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>
