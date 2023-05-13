<template>
  <Header />
  <h1>Hello {{ name }}, Welcome on Home Page</h1>
  <table border="1">
    <tr>
      <td>ID</td>
      <td>Name</td>
      <td>Contact</td>
      <td>Address</td>
      <td>Actions</td>
    </tr>
    <tr v-for="item in restaruant" :key="item.id">
      <td>{{ item.id }}</td>
      <td>{{ item.name }}</td>
      <td>{{ item.contact }}</td>
      <td>{{ item.address }}</td>
      <td>
        <router-link :to="'/update/' + item.id">Update</router-link>
        <button v-on:click="deleteRestaurant(item.id)">Delete</button>
      </td>
    </tr>
  </table>
</template>

<script>
import Header from "./Header.vue";
import axios from "axios";

export default {
  name: "HomePage",
  data() {
    return {
      name: "",
      restaruant: [],
    };
  },
  components: {
    Header,
  },
  methods: {
    async deleteRestaurant(id) {
      console.warn(id);
      const result = await axios.delete(
        "http://localhost:3000/restaurant/" + id
      );
      if (result.status === 201) {
        this.$router.push({ name: "Home" });
      } else {
        this.name = JSON.parse(localStorage.getItem("user-info")).name;
        if (!localStorage.getItem("user-info")) {
          this.$router.push({ name: "SignUp" });
        }
        let result = await axios.get("http://localhost:3000/restaurant");
        this.restaruant = result.data;
      }
    },
  },
  async mounted() {
    this.name = JSON.parse(localStorage.getItem("user-info")).name;
    if (!localStorage.getItem("user-info")) {
      this.$router.push({ name: "SignUp" });
    }
    let result = await axios.get("http://localhost:3000/restaurant");
    this.restaruant = result.data;
  },
};
</script>

<style>
td {
  width: 160px;
  height: 40px;
}
</style>
