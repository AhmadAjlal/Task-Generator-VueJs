<template>
  <footer>
    <p>Copyright &copy; 2023 | All Rights Reserved @Ahmad</p>
    <router-link v-show="!aboutPage" to="/about">About Us</router-link>
    <router-link v-show="aboutPage" to="/">Go Back</router-link>
  </footer>

</template>

<script>
export default {
  name: "FooterComponent",
  computed: {
    aboutPage() {
      if (this.$route.path === '/about') {
        return true;
      } else {
        return false;
      }
    }
  },
}
</script>

<style scoped>
a {
  color: #333;
}

footer {
  margin-top: 30px;
  text-align: center;
}
</style>