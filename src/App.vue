<template>
  <div id="app">
    <Request1 />
    <Request2 />
  </div>
</template>

<script>
import Request1 from "./components/Request1.vue";
import Request2 from "./components/Request2.vue";

export default {
  name: "App",
  components: {
    Request1,
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
