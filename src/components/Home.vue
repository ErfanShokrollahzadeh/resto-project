<template>
  <h1>Hello User, Welcome on Home Page</h1>
</template>

<script>
export default {
  name: "HomePage",
   mounted() {
    if(!localStorage.getItem("user-info")) {
      this.$router.push({name: "SignUp"});
    }
  }
};
</script>
