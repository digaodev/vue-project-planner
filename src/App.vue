<template>
  <NavBar></NavBar>
  <router-view />
</template>

<script>
import NavBar from "./components/NavBar.vue";

export default {
  components: { NavBar },
};
</script>

<style>
body {
  background: #f2f2f2;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #555;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  margin: 0 auto;
  max-width: 600px;
}
.main-nav {
  text-align: center;
  margin: 40px auto;
}
.main-nav a {
  display: inline-block;
  text-decoration: none;
  margin: 0 10px;
  color: #777;
  font-size: 18px;
}
a.router-link-active {
  border-bottom: 2px solid #00ce89;
  color: #333;
  padding-bottom: 4px;
}
</style>
