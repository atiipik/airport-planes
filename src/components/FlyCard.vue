<template>
  <div class="card-airport">
    <div class="wrapper">
      <div>
        <p class="big-text">JFK</p>
        <p class="small-text">New York, John F. Kennedy International</p>
      </div>
      <img class="plane" src="@/assets/plane.gif" alt="icon avion" />
      <div class="right">
        <p class="big-text">CDG</p>
        <p class="small-text">Paris, Charles de Gaulle</p>
      </div>
    </div>
    <img class="logo-compagny" src="https://api.joshdouch.me/logos/ABR.bmp" alt="logo compagnie" />
    <div class="wrapper">
      <div>
        <p class="small-text">Départ</p>
        <p class="big-text">01:54</p>
      </div>
      <div class="right">
        <p class="small-text">Arrivé</p>
        <p class="big-text">10:23</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {};
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