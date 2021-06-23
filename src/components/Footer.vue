<template>
  <footer>
    <p>Copyright &copy; 2021</p>
    <router-link to="/about">About</router-link>
  </footer>
</template>

<script lang="ts">
export default {
  name: "Footer",
};
</script>

<style lang="scss" scoped>
footer {
  margin-top: 30px;
  text-align: center;
}

a {
  color: #333;
}
</style>