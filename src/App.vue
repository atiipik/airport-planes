<template>
  <div>
    <button @click="direction">Arrivées ↘️</button>
    <button @click="direction = false">Départs ↗️</button>
    <input class="btn-date" type="date" v-model="begin" />
    <input class="btn-date" type="date" v-model="end" />
    <input class="btn-airport" list="airports" v-model="airport" />
    <datalist id="airports">
      <option
        v-for="(airport, index) in allAirports"
        :key="index"
        :value="airport.iata"
      >
        {{ airport.name }}
      </option>
    </datalist>

    <button @click="getFlightByDateAndAirport()">Vols ✈️</button>
    <pre>{{ openSky }}</pre>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: "App",
  components: {
    // HelloWorld
  },

  data() {
    return {
      openSky: null,
      direction: true, //* true = arrival, false = departure
      airport: "",
      begin: "",
      end: "",
      allAirports: [
      { iata: "CDG", name: "Paris, Charles de Gaulle" }, 
      { iata: "LIL", name: "Lille, Lesquin" }, 
      { iata: "ORY", name: "Paris, Orly" }, 
      { iata: "NCE", name: "Nice, Côte d'Azur" }, 
      { iata: "LYS", name: "Lyon, Saint-Exupéry" }, 
      { iata: "MRS", name: "Marseille, Provence" }, 
      { iata: "TLS", name: "Toulouse, Blagnac" }, 
      { iata: "BOD", name: "Bordeaux, Mérignac" }, 
      { iata: "NTE", name: "Nantes, Atlantique" }, 
      { iata: "PTP", name: "Guadeloupe, Pôle Caraïbes" }, 
      { iata: "MPL", name: "Montpellier, Méditerranée" }, 
      { iata: "ATL", name: "Atlanta, Atlanta H.-Jackson" }, 
      { iata: "PEK", name: "Pékin, Capitale" }, 
      { iata: "LAX", name: "Los Angeles, Los Angeles" }, 
      { iata: "DXB", name: "Dubaï, Dubaï" }, 
      { iata: "LHR", name: "Londres, Heathrow" }, 
      { iata: "HKG", name: "Hong Kong, Hong Kong" }, 
      { iata: "JFK", name: "New York, John F. Kennedy" }, 
      { iata: "DEL", name: "Delhi, Indira Gandhi" }, 
      ],
    };
  },
  mounted() {},
  methods: {
    async getIcao(iata) {
      const axios = require("axios");
      let res = await axios
        .get(`https://api.joshdouch.me/IATA-ICAO.php?iata=${iata}`)
        return res.data
      
    },
    async getFlightByDateAndAirport() {
      let iaco = await this.getIcao(this.airport)
      const axios = require("axios");
      axios
        .get(
          `https://opensky-network.org/api/flights/${this.direction ? "arrival" : "departure"}?airport=${iaco}&begin=${Date.parse(this.begin) / 1000}&end=${Date.parse(this.end) / 1000}`)
        .then((response) => (this.openSky = response));
    },
  },
};
</script>

<style></style>
