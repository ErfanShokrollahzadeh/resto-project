<template>
  <Header />
  <h1>Hello User, Welcome on Add Restaurant Page</h1>
  <form class="add">
    <input
      type="text"
      name="name"
      placeholder="Enter Name"
      v-model="restaurant.name"
    />
    <input
      type="text"
      name="address"
      placeholder="Enter address"
      v-model="restaurant.address"
    />
    <input
      type="text"
      name="contact"
      placeholder="Enter contact"
      v-model="restaurant.contact"
    />
    <button type="button" v-on:click="addRestaurant">Add New Restaurant</button>
  </form>
</template>

<script>
import Header from "./Header.vue";
import axios from "axios";

export default {
  name: "AddPage",
  components: {
    Header,
  },
  data() {
    return {
      restaurant: [
        {
          name: "",
          address: "",
          contact: "",
        },
      ],
    };
  },
  methods: {
    async addRestaurant() {
      console.warn(this.restaurant);
      const result = await axios.post("http://localhost:3000/restaurant", {
        name: this.restaurant.name,
        address: this.restaurant.address,
        contact: this.restaurant.contact,
      });
      if (result.data.status === 200) {
        this.$router.push({ name: "Home" });
      } else {
        this.$router.push({ name: "Home" });
      }
      console.warn("result",result);
    },
  },
  mounted() {
    if (!localStorage.getItem("user-info")) {
      this.$router.push({ name: "SignUp" });
    }
  },
};
</script>
