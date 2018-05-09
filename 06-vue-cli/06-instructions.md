# Vue Lunch & Learn

## Part 06 - Use the vue-cli

### Instructions

> Vue provides an official CLI for quickly scaffolding ambitious Single Page Applications. It provides batteries-included build setups for a modern frontend workflow. It takes only a few minutes to get up and running with hot-reload, lint-on-save, and production-ready builds.

* Install the `vue-cli` globally

```
npm install -g @vue/cli
```

* Open terminal, navigate to /code, then create a new vue project with the cli

```
vue create vue-weather
```

* `cd` into the directory and open it in code with `code .`
* explore the file structure a bit

* add bootstrap to the index.html file

```html
  <!-- Bootstrap CSS -->
  <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.1/css/bootstrap.min.css" integrity="sha384-WskhaSGFgHYWDcbwN70/dfYBj47jz9qbsMId/iRN3ewGhXQFZCSftd1LZCfmhktB"
    crossorigin="anonymous">

  <title>Vue Weather</title>
```

* replace the App content with our static content

```html
  <header>
    <div class="navbar navbar-dark bg-dark box-shadow">
      <div class="container d-flex justify-content-between">
        <a href="#" class="navbar-brand d-flex align-items-center">
          <strong>Vue Weather</strong>
        </a>
      </div>
    </div>
  </header>
```

* remove `HelloWord` from App component

```js
<script>
import CityCard from "./components/CityCard.vue";

export default {
  name: "app",
  components: {
    CityCard
  }
};
</script>
```

* add a `CityCard.vue` component in the /components folder

```js
<template>
  <div>I am a CityCard Component</div>
</template>

<script>
</script>

<style scoped>
</style>
```

* copy the CityCard component contents into the new single file template

```html
  <div class="card">
    <div class="card-body">
      <h5 class="card-title">{{ cityName }}</h5>
      <h6 class="card-subtitle mb-2 text-muted">Now: {{ tempF }}&deg; - {{ weatherDesc }}</h6>
      <button type="button" class="btn btn-primary" v-on:click="toggleForecast">{{showForecast ? 'Hide' : 'Show'}} Forecast</button>
      <div v-if="showForecast">
        <p class="card-text">
          <p>Five-day Forecast (avg: {{ fiveDayAverageTemp }}&deg;)</p>
          <p v-for="forecast in forecastFiveDays">
            <b>{{ forecast.temp }}&deg;</b>
            <br />
            <em>{{ forecast.weatherDesc }}</em>
            <br />
            <small>{{ forecast.timestamp }}</small>
          </p>
        </p>
      </div>
    </div>
  </div>
```

```js
<script>
export default {
  props: {
    cityName: {
      type: String,
      required: true
    },
    tempF: {
      type: String,
      required: true
    },
    weatherDesc: {
      type: String,
      required: true
    },
    fiveDayAverageTemp: {
      type: Number,
      required: true
    },
    forecastFiveDays: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      showForecast: false
    };
  },
  methods: {
    toggleForecast() {
      this.showForecast = !this.showForecast;
    }
  }
};
</script>
```

* Notice the red squigglies! Now we get linting errors

* Update App.vue with all of the top level stuff

```html
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
```

```js
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
```

* Deploy to Netlify?
