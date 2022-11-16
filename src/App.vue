<template>
  <div id="app">
    <h1>Hello there!</h1>
  </div>
</template>

<script>
import WeatherKey from './keys/open-weather.txt'

export default {
  name: 'App',
  components: {
    // HelloWorld
  },
  data() {
    return {
      key: WeatherKey,
    }
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
