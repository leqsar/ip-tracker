<script setup>
import Form from "./components/Form.vue";
import Result from "./components/Result.vue";
import Map from "./components/Map.vue";
</script>

<script>
export default {
  data() {
    return {
      ip: "",
      location: "",
      timezone: "",
      isp: "",
      center: [0, 0],
      error: false
    };
  },
  mounted() {
    fetch('https://api.ipify.org?format=json')
      .then(response => response.json())
      .then(data => this.ip = data.ip);
  },
  methods: {
    setIp(chosenIp) {
      const format = new RegExp(/^(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$/);
      if(format.test(chosenIp)) {
        this.error = false;
        this.ip = chosenIp;
      } else {
        this.error = true;
      }
    },
    getLocationInfo(ip) {
      const url = `https://geo.ipify.org/api/v2/country,city?apiKey=${import.meta.env.VITE_API_KEY}&ipAddress=${ip}`;
      fetch(url)
        .then((response) => {
          if (!response.ok) {
            throw new Error(`HTTP error: ${response.status}`);
          }
          return response.json();
        })
        .then((data) => {
          this.location = `${data.location.city}, ${data.location.region}, ${data.location.postalCode}`;
          this.timezone = data.location.timezone;
          this.isp = data.isp;
          const lngLatArray = [];
          lngLatArray.push(data.location.lng);
          lngLatArray.push(data.location.lat);
          this.center = lngLatArray;
        })
        .catch((error) => {});
    },
  },
  watch: {
    ip(newIp) {
      this.getLocationInfo(newIp);
    },
  },
};
</script>

<template>
  <Form @submit-form="setIp" :error="error"/>
  <Result :ip="ip" :location="location" :isp="isp" :timezone="timezone" :center="center"/>
  <Map :center="center"/>
  <div class="attribution">
    Challenge by <a href="https://www.frontendmentor.io?ref=challenge" target="_blank">Frontend Mentor</a>. 
    Coded by <a href="https://github.com/leqsar">leqsar</a>.
  </div>
</template>

<style scoped lang="sass">
  @import "./input.sass"
  .attribution
    margin-top: 10px
    color: $veryDarkGray

    a
      text-decoration: none
      color: $darkGray
</style>
