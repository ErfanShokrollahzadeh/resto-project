<template>
  <img src="../assets/resto-logo.webp" class="logo" />
  <h1>Sign Up</h1>
  <div class="register">
    <input type="text" v-model="name" placeholder="Enter Name" />
    <input type="text" v-model="email" placeholder="Enter Email" />
    <input type="password" v-model="password" placeholder="Enter Password" />
    <button v-on:click="signUp">Sign Up</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
    name: "SignUp",
    data() { 
        return {
            name: "",
            email: "",
            password: "",
        }
    },
    methods: {
        async signUp() {
            let result = await axios.post("http://localhost:3000/user", {
                name: this.name,
                email: this.email,
                password: this.password,
            });

            console.warn(result);
            if(result.data.status === "success") {
                alert("Sign Up Success");
                this.$router.push("/login");
            } else {
              localStorage.setItem("user-info", JSON.stringify(result.data));
              this.$router.push({name: "Home"});

            }
        }
  },
  mounted() {
    if(localStorage.getItem("user-info")) {
      this.$router.push({name: "Home"});
    }
  }
};
</script>

<style>
.logo {
  width: 160px;
  height: 160px;
}
.register input {
  width: 300px;
  height: 40px;
  padding-left: 20px;
  display: block;
  margin-bottom: 30px;
  margin-right: auto;
  margin-left: auto;
  border: 1px solid #e081ba;
}
.register button {
  width: 320px;
  height: 40px;
  border: 1px solid skyblue;
  background-color: #04b271;
  color: #fff;
  cursor: pointer;
}
</style>
