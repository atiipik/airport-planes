<template>
  <div class="card-airport">
    <div class="wrapper">
      <div>
        <p class="big-text">{{ iataDepart }}</p>
        <p class="small-text">{{ cityDepart }}</p>
      </div>
      <div>
        <img class="plane" src="@/assets/plane.gif" alt="icon avion" />
      </div>
      <div class="right">
        <p class="big-text">{{ iataArrival }}</p>
        <p class="small-text">{{ cityArrival }}</p>
      </div>
    </div>
    <div class="separator"></div>
    <div class="wrapper">
      <div>
        <p class="small-text">Départ</p>
        <p class="big-text">{{departTime}}</p>
      </div>
      <img
        :onerror="isError()"
        class="logo-compagny"
        :src="urlLogo"
        alt="logo compagnie"
      />
      <!-- <p>{{urlLogo}}</p> -->
      <div class="right">
        <p class="small-text">Arrivé</p>
        <p class="big-text">{{arrivalTime}}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      imgError: false,
      departAirporta: this.departAirport,
      arrivalAirporta: this.arrivalAirport,
      icao24hex: this.icao24,
      urlLogo: "",
      iataDepart: "",
      iataArrival: "",
      IataDepart: "",
      IataArrival: "",
      cityDepart: "",
      cityArrival: "",
    };
  },
  props: ["departAirport", "arrivalAirport", "icao24", "departTime", "arrivalTime"],
  mounted() {
    const depart = require("axios");
    depart
      .get(
        `https://api.joshdouch.me/ICAO-airport.php?icao=${this.departAirporta}`
      )
      .then((response) => (this.cityDepart = response.data));

    const arrival = require("axios");
    arrival
      .get(
        `https://api.joshdouch.me/ICAO-airport.php?icao=${this.arrivalAirporta}`
      )
      .then((response) => (this.cityArrival = response.data));

    const compagny = require("axios");
    compagny
      .get(`https://api.joshdouch.me/hex-logo.php?hex=${this.icao24hex}`)
      .then((response) => (this.urlLogo = response.data));

    const iataDepart = require("axios");
    iataDepart
      .get(`https://api.joshdouch.me/ICAO-IATA.php?icao=${this.departAirporta}`)
      .then((response) => (this.iataDepart = response.data));

    const iataArrival = require("axios");
    iataArrival
      .get(
        `https://api.joshdouch.me/ICAO-IATA.php?icao=${this.arrivalAirporta}`
      )
      .then((response) => (this.iataArrival = response.data));
  },
  methods: {
    isError() {
      console.log("il y a erreur monsieur");
    },
  },
};
</script>

<style scoped>
.card-airport {
  background-color: #ffffff;
  border-radius: 2.415vw;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 4.348vw;
  gap: 4.348vw;
}

p {
  margin: 0;
}
.wrapper {
  width: 100%;
  height: fit-content;
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
}

.wrapper > div {
  width: calc(100% / 3);
}

.wrapper > div:nth-child(2) {
  display: flex;
  align-items: center;
  justify-content: center;
}

.card-airport div:nth-child(3) {
  align-items: center;
}

.separator {
  background-color: rgba(0, 0, 0, 0.25);
  width: 100%;
  height: 1px;
}

.right {
  text-align: right;
}

.plane {
  width: 4.831vw;
  margin-top: 1.932vw;
  opacity: 0.8;
}
.wrapper div {
  max-width: 20.531vw;
}

.big-text {
  color: blue;
  font-size: 5.797vw;
  font-family: "Urbanist-Black", sans-serif;
  letter-spacing: 0.121vw;
  margin-bottom: 0.966vw;
}

.small-text {
  color: rgba(0, 0, 0, 0.5);
  font-size: 1.932vw;
  font-family: "Urbanist", sans-serif;
}

.logo-compagny {
  height: 3.623vw;
}
</style>
