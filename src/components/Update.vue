<template>
  <Header />
  <h1>Hello User, Welcome on Update Restaurant Page</h1>
</template>

<script>
import Header from "./Header.vue";

export default {
  name: "UpdatePage",
  components: {
    Header,
  },
  mounted() {
    if (!localStorage.getItem("user-info")) {
      this.$router.push({ name: "SignUp" });
    }
  },
};
</script>
