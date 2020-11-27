<template>
  <div id="app">
    <Request />
    <Request2 />
  </div>
</template>

<script>
import Request from "./components/Request.vue";
import Request2 from "./components/Request2.vue";

export default {
  name: "App",
  components: {
    Request
    // Request2
  }
};
</script>

<style>
#app {
  font-family: Arial, Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

h1 {
  padding-top: 50px;
  color: black;
}

html {
  height: 97.5%;
  padding-right: 16px;
  padding-left: 16px;
}

html {
  background: white;
}

body {
  margin: 0px;
  background-color: #aaa;
  border-radius: 50px;
  height: 97.5%;
}
</style>
