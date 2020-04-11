<template>
  <div id="app">
    <Labirint />
  </div>
</template>

<script>
import Labirint from "./components/Labirint";

export default {
  name: "App",
  components: {
    Labirint
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
