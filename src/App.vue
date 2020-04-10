<template>
  <div id="app">
    <About />
    <Request2 />
  </div>
</template>

<script>
import About from "./components/About.vue";
import Request2 from "./components/Request2.vue";

export default {
  name: "App",
  components: {
    About,
    Request2
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
