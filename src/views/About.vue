<template>
  <div id="app">
    <h1>Bitcoin Price Index</h1>

    <section v-if="errored">
      <p>
        We're sorry, we're not able to retrieve this information at the moment,
        please try back later
      </p>
    </section>

    <section v-else>
      <div v-if="loading">Loading...</div>

      <div v-else v-for="data in info" :key="data" class="currency">
        <h1>{{ data.Portugal[0].deaths }}</h1>
      </div>
    </section>
  </div>
</template>

<script>
import axios from "axios";
import Vue from "vue";

new Vue({
  el: "#app",
  data() {
    return {
      info: null,
      loading: true,
      errored: false
    };
  },
  mounted() {
    axios
      .get("https://pomber.github.io/covid19/timeseries.json")
      .then(response => {
        this.info = response.data;
        console.log(this.info);
      })
      .catch(error => {
        console.log(error);
        this.errored = true;
      })
      .finally(() => (this.loading = false));
  }
});

export default {
  name: "About",
  props: {
    loading: String,
    errored: String,
    info: String
  }
};
</script>
