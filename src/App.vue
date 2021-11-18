<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Navbar</a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarSupportedContent"
          aria-controls="navbarSupportedContent"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <a v-if="!isLoggedIn()" class="nav-link active" aria-current="page" href="#">Home</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="/about">About</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="/test">Test</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="/posts">All Posts</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="/posts/new">New Post</a>
            </li>
            <li class="nav-item dropdown">
              <a
                class="nav-link dropdown-toggle"
                href="#"
                id="navbarDropdown"
                role="button"
                data-bs-toggle="dropdown"
                aria-expanded="false"
              >
                Account
              </a>
              <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
                <li><a v-if="!isLoggedIn()" class="dropdown-item" href="/signup">Signup</a></li>
                <li><a v-if="!isLoggedIn()" class="dropdown-item" href="/login">Login</a></li>
                <li><hr class="dropdown-divider" /></li>
                <li><a v-if="isLoggedIn()" class="dropdown-item" href="/logout">Logout</a></li>
              </ul>
            </li>
          </ul>
          <form class="d-flex">
            <input
              class="form-control me-2"
              type="search"
              placeholder="Search by title"
              aria-label="Search"
              input-type="text"
              v-model="titleFilter"
            />
          </form>
        </div>
      </div>
    </nav>
    <!-- <div v-if="flashMessage" v-on:click="flashMessage ''" class="alert alert-sucess">{{ flashMessage }}</div> -->
    <router-view />
  </div>
</template>

<style>
body {
  background-image: url(./assets/webb-dark.png);
  color: darkcyan;
}
p {
  text-align: center;
  font-family: Copperplate, "Copperplate Gothic Light";
  color: aqua;
}

h1 {
  text-align: center;
  font-family: Copperplate, "Copperplate Gothic Light", fantasy;
  font-size: 24px;
  font-style: normal;
  font-variant: normal;
  font-weight: 700;
  line-height: 26.4px;
  color: darkcyan;
}

h2 {
  text-align: center;
  font-family: Copperplate, "Copperplate Gothic Light", fantasy;
  font-size: 18px;
  font-style: normal;
  font-variant: normal;
  font-weight: 600;
  line-height: 25px;
  color: darkcyan;
}

img {
  align-content: center;
  color: aliceblue;
}

label {
  color: aqua;
}

button {
  align-content: center;
}
</style>

<script>
export default {
  data: function () {
    return {
      // flashMessage: "",
      titleFilter: "",
    };
  },
  methods: {
    isLoggedIn: function () {
      if (localStorage.getItem("jwt")) {
        return true;
      } else {
        return false;
      }
    },
    getUserId: function () {
      return localStorage.getItem("user_id");
    },
  },
};
</script>
