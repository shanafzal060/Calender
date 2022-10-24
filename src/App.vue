<template>
  <VueCalender />
</template>

<script>
import VueCalender from "./components/VueCalender.vue";

export default {
  name: "App",
  components: {
    VueCalender,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
