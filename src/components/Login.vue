<template>
  <img src="../assets/resto-logo.webp" class="logo" />
  <h1>Login</h1>
  <div class="login">
    <!-- <input type="text" v-model="name" placeholder="Enter name" /> -->
    <input type="text" v-model="email" placeholder="Enter Email" />
    <input type="password" v-model="password" placeholder="Enter Password" />
    <button v-on:click="login">Login</button>
    <p><router-link to="/sign-up">Sing Up</router-link></p>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "LoginPage",
  data() {
    return {
      name: "",
      email: "",
      password: "",
    };
  },
  methods: {
    async login() {
      let result = await axios.post("http://localhost:3000/user", {
        // name: this.name,
        email: this.email,
        password: this.password,
      });

      console.warn(result);
      if (result.data.status === "success") {
        this.$router.push("/login");
      } else {
        localStorage.setItem("user-info", JSON.stringify(result.data));
        this.$router.push({ name: "Home" });
      }
    },
  },
  mounted() {
    if (localStorage.getItem("user-info")) {
      this.$router.push({ name: "Home" });
    }
  },
};
</script>
