<template>
  <div id="app">
    <About />
  </div>
</template>

<script>
import About from "./components/About.vue";

export default {
  name: "App",
  components: {
    About
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
</style>
