<template>
  <div id="app">
  <header>
    <div class="navbar navbar-dark bg-dark box-shadow">
      <div class="container d-flex justify-content-between">
        <a href="#" class="navbar-brand d-flex align-items-center">
          <strong>Vue Weather</strong>
        </a>
      </div>
    </div>
  </header>
  <main role="main">

    <section class="jumbotron text-center">
      <div class="container">
        <h1 class="jumbotron-heading">Vue Weather</h1>
        <p class="lead text-muted">Learning Vue by making a weather app</p>
      </div>
    </section>

    <section id="app" class="container">
      <div class="form-group mb-4">
        <label for="citySelect">Select a city</label>
        <select v-model="cityName" v-on:change="fetchData" class="form-control" id="citySelect">
          <option>Atlanta</option>
          <option>London</option>
          <option>Tokyo</option>
          <option>San Francisco</option>
          <option>Cairo</option>
        </select>
      </div>

      <CityCard :city-name="cityName" :temp-f="tempF" :weather-desc="weatherDesc" :five-day-average-temp="fiveDayAverageTemp"
        :forecast-five-days="forecastFiveDays"></CityCard>
    </section>

  </main>
  </div>
</template>

<script>
import CityCard from "./components/CityCard.vue";

var OWM_CURRENT_URL = "api.openweathermap.org/data/2.5/weather";
var OWM_FORECAST_URL = "api.openweathermap.org/data/2.5/forecast";
var OWM_API_KEY = "4dcdc5ef8f4820617031f0658196dcba";

export default {
  name: "app",
  components: {
    CityCard
  },
  data() {
    return {
      showForecast: false,
      cityName: "Atlanta",
      tempF: 75,
      weatherDesc: "Sunny",
      forecastFiveDays: []
    };
  },
  created() {
    this.fetchData();
  },
  methods: {
    fetchData: function() {
      return this.fetchCurrentWeather().then(() => this.fetchFiveDayForecast());
    },
    fetchCurrentWeather: function() {
      return fetch(
        `http://${OWM_CURRENT_URL}?q=${
          this.cityName
        }&units=imperial&APPID=${OWM_API_KEY}`
      )
        .then(response => response.json())
        .then(data => {
          if (data.cod == 200 && data.main) {
            this.tempF = data.main.temp;
            this.weatherDesc = data.weather[0].description;
          }
          console.log("Fetched current weather from OpenWeatherMap:");
          console.log(data);
        })
        .catch(err => {
          console.warn(err);
        });
    },
    fetchFiveDayForecast: function() {
      return fetch(
        `http://${OWM_FORECAST_URL}?q=${
          this.cityName
        }&units=imperial&APPID=${OWM_API_KEY}`
      )
        .then(response => response.json())
        .then(data => {
          if (data.list && data.list.length > 0) {
            this.forecastFiveDays = data.list.map(f => {
              return {
                timestamp: new Date(f.dt_txt).toString(),
                temp: f.main.temp,
                weatherDesc: f.weather[0].description
              };
            });
          }
          console.log("Fetched forecase from OpenWeatherMap:");
          console.log(data);
        })
        .catch(err => {
          console.warn(err);
        });
    }
  },
  computed: {
    fiveDayAverageTemp: function() {
      return Math.round(
        this.forecastFiveDays.reduce((acc, curr) => acc + curr.temp, 0) /
          this.forecastFiveDays.length
      );
    }
  }
};
</script>

<style>

</style>
