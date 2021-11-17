<template>
  <div class="postnew">
    <img v-if="status" :src="`https://http.cat/${status}`" alt="" />
    <form v-on:submit.prevent="createPost()">
      <h1>{{ message }}</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newPostParams.title" />
      </div>
      <div>
        <label>Body:</label>
        <input type="text" v-model="newPostParams.body" />
        <small>{{ 100 - newPostParams.body.length }}</small>
        <small v-if="newPostParams.body.length > 100" class="text-danger">
          You have exceeded the number of characters
        </small>
      </div>
      <div>
        <label>Image:</label>
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
      newPostParams: { body: "" },
      errors: [],
      status: "",
    };
  },
  methods: {
    createPost: function () {
      axios
        .post("/posts", this.newPostParams)
        .then(() => {
          this.$router.push("/posts");
        })
        .catch((error) => {
          this.status = error.response.status;
          console.log(error.response);
        });
    },
  },
};
</script>
