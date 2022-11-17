<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 60 ? 'warm' : ''">
    <main>
      <h1>Vue-Weather</h1>
      <div class="search-box">
        <input type="text" class="search-bar" placeholder="Search for weather" v-model="query"
               @keypress="fetchWeather"/>
      </div>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location"><h1>{{ weather.name }}</h1></div>
          <div class="date"><h2>{{ dateBuilder() }}</h2></div>
        </div>
        <div class="weather-box">
          <div class="temp">
            <h2>{{ Math.round(weather.main.temp) }}°F</h2>
            <div class="weather">
              <h3>{{ weather.weather[0].main }}</h3>
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import WeatherKey from './keys/open-weather.txt'

export default {
  name: 'App',
  components: {},
  data() {
    return {
      api_key: WeatherKey,
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {},
    }
  },
  methods: {
    async fetchWeather(e) {
      const url = `${this.url_base}weather?q=${this.query}&date&units=imperial&appid=${this.api_key}`
      if (e.key === "Enter") {
        fetch(url)
            .then(res => {
              return res.json();
            }).then(this.setResults);
      }
    },
    setResults(results) {
      this.weather = results;
      console.log(results)
    },
    dateBuilder() {
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
    }
  }
}
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: papayawhip;
  background-image: url('./assets/cold-bg.jpg');
  background-size: contain;
  background-position: center;
  background-repeat: round;
  transition: 0.4s;
}

#app.warm {
  background-image: url('./assets/warm-bg.jpg');
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'montserrat', sans-serif;
}

main {
  min-height: 100vh;
  padding: 20px 25px 25px;
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
}

.search-bar {
  text-align: center;
}

.search-box {
  width: 100%;
  margin-bottom: 10px;
}

.search-box .search-bar {
  display: block;
  width: 75vw;
  height: 10vh;
  margin: 10px auto auto;
  padding: 15px;
  color: papayawhip;
  font-size: 16px;
  appearance: none;
  border: none;
  outline: none;
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background: rgba(255, 255, 255, 0.6) none;
  border-radius: 16px 16px 16px 16px;
  transition: 0.75s;
}

.search-box .search-bar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 16px 16px 16px;
}

.location-box .location {
  color: papayawhip;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.location-box .date {
  color: papayawhip;
  text-align: center;
}

.weather-box {
  text-align: center;
}

.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: papayawhip;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px;
  margin-top: 10px;
  margin-bottom: 10px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.weather-box .weather {
  color: papayawhip;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
