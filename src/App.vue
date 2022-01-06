<template>
  <div>
    <pre>{{ openSky }}</pre>
    <button @click="direction">Arrivées ↘️</button>
    <button @click="direction = false">Départs ↗️</button>
    <input class="btn-date" type="text" v-model="begin" />
    <input class="btn-date" type="text" v-model="end" />
    <input class="btn-airport" type="text" v-model="airport" />
    <button @click="getFlightByDateAndAirport()">Vols ✈️</button>

    <FlyCard />
  </div>
</template>

<script>
import FlyCard from "./components/FlyCard.vue";

export default {
  name: "App",
  components: {
    FlyCard,
  },

  data() {
    return {
      openSky: null,
      direction: true, //* true = arrival, false = departure
      airport: "LFPG",
      begin: "1641339245",
      end: "1641425645",
    };
  },
  mounted() {},
  methods: {
    getFlightByDateAndAirport() {
      const axios = require("axios");
      axios
        .get(
          `https://opensky-network.org/api/flights/${
            this.direction ? "arrival" : "departure"
          }?airport=${this.airport}&begin=${this.begin}&end=${this.end}`
        )
        .then((response) => (this.openSky = response));
    },
  },
};
</script>

<style>
html {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body {
  background-color: rgb(240, 233, 233);
  padding: 5.797vw 4.348vw;
}
</style>
