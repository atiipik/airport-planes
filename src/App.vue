<template>
  <div></div>
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
    };
  },
  mounted() {
    axios
      .get("https://api.coindesk.com/v1/bpi/currentprice.json")
      .then((response) => (this.openSky = response));
  },
};
</script>

<style>
</style>
