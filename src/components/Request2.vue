<script>
import axios from "axios";
import CountryChart2 from "./WHOChart.vue";

export default {
  name: "Request2",
  components: {
    CountryChart2
  },
  data: () => ({
    info: null,
    loading: true,
    errored: false,
    country: null
  }),
  mounted() {
    axios
      .get("https://corona-api.com/countries")
      .then(response => {
        this.info = response.data.data;
        let listOfObjects = Object.keys(this.info).map(key => {
          console.log("Request 2 type of response", typeof this.info[key]);
          return this.info[key];
        });
      })
      .catch(error => {
        this.errored = true;
      })
      .finally(() => (this.loading = false));
  }
};
</script>

<template>
  <div>
    <h1>World Health Organization Covid-19 cases by Country</h1>
    <section v-if="errored">
      <p>
        We're sorry, we're not able to retrieve this information at the moment,
        please try back later
      </p>
    </section>

    <section v-else>
      <div v-if="loading">Loading...</div>
      <div v-else>
        <select v-model="country" class="option">
          <option :value="null">-- Select Country --</option>
          <option v-for="value in info" :key="value.code">
            {{ value.name }}
          </option>
        </select>
        <div v-if="country">
          <CountryChart2 :countrydata2="country.value" />
        </div>
      </div>
    </section>
  </div>
</template>

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
