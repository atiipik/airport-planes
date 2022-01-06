<template>
  <div>
    <div class="btn-wrapper">
      <button class="btn" @click="direction = false">Départs ↗️</button>
      <button class="btn" @click="direction">Arrivées ↘️</button>
    </div>
    <div class="btn-wrapper">
      <input class="btn" type="date" v-model="begin" />
      <input class="btn" type="date" v-model="end" />
    </div>
    <div class="btn-wrapper">
      <input class="btn" list="airports" v-model="airport" />
      <datalist id="airports">
        <option
          v-for="(airport, index) in allAirports"
          :key="index"
          :value="airport.iata"
        >
          {{ airport.name }}
        </option>
      </datalist>

      <button @click="getFlightByDateAndAirport()">
        Rechercher un vols ✈️
      </button>
    </div>

    <!-- <p>{{openSky}}</p> -->

    <FlyCard :departAirport="airport.estDepartureAirport" :arrivalAirport="airport.estArrivalAirport" :icao24="airport.icao24" v-for="(airport, index) in openSky" :key="index"/>
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
      let res = await axios.get(
        `https://api.joshdouch.me/IATA-ICAO.php?iata=${iata}`
      );
      return res.data;
    },
    async getFlightByDateAndAirport() {
      let iaco = await this.getIcao(this.airport);
      const axios = require("axios");
      axios
        .get(
          `https://opensky-network.org/api/flights/${
            this.direction ? "arrival" : "departure"
          }?airport=${iaco}&begin=${Date.parse(this.begin) / 1000}&end=${
            Date.parse(this.end) / 1000
          }`
        )
        .then((response) => (this.openSky = response.data));
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

.card-airport:not(:last-child) {
  margin-bottom: 5.797vw;
}

.btn-wrapper {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 5.797vw;
}

.btn-wrapper:last-child {
  margin-bottom: 8.696vw;
}

.btn {
  width: 38.406vw;
  text-transform: uppercase;
  font-size: 12px;
}
</style>
