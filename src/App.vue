<template>
  <div id="app">
    <app-header />
    <router-view />
    <app-footer />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";

export default {
  components: {
    "app-header": Header,
    "app-footer": Footer,
  },
};
</script>

<style lang="scss">
#app {
  background-color: rgb(221, 234, 240);
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  // color: #2c3e50;
}
</style>
