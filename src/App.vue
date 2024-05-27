<template>
  <div id="app">
    <WeatherSite/>
  </div>
</template>

<script>
import WeatherSite from './components/WeatherSite.vue'

export default {
  name: 'App',
  components: {
    WeatherSite
  }
}
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
