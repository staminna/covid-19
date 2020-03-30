<template>
  <div>
    <h1>Covid-19 cases by Country</h1>
    <section v-if="errored">
      <p>
        We're sorry, we're not able to retrieve this information at the moment,
        please try back later
      </p>
    </section>

    <section v-else>
      <div v-if="loading">Loading...</div>
      <div v-else>
        <select v-model="country">
          <option :value="null">-- no selection --</option>
          <option
            v-for="(data, name) in info"
            :value="{ data, name }"
            :key="name"
            v-text="name"
          ></option>
        </select>
        <div v-if="country">
          <CountryChart :countrydata="country.data" />
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import axios from "axios";
import CountryChart from "./Chart.vue";

export default {
  name: "About",
  components: {
    CountryChart
  },
  data: () => ({
    info: null,
    loading: true,
    errored: false,
    country: null
  }),
  mounted() {
    axios
      .get("https://pomber.github.io/covid19/timeseries.json")
      .then(response => {
        this.info = response.data;
        // console.log(this.info);
      })
      .catch(error => {
        this.errored = true;
      })
      .finally(() => (this.loading = false));
  }
};
</script>
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
