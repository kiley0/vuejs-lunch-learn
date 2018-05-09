# Vue Lunch & Learn

## Part 02 - Conditionals and Loops

### Instructions

* Continue editing `index.html`
* Add a few `p` tags below the current temp

```html
<p v-if="tempF >= 90" class="lead">It's hot outside!</p>
```

* Change the temp in the console and show v-if directive working
* Add the following below the first v-if

```html
<p v-else-if="tempF >= 80 && tempF < 90" class="lead">It's warm outside</p>
<p v-else-if="tempF >= 70 && tempF < 80" class="lead">It's comfortable outside</p>
<p v-else-if="tempF >= 40 && tempF < 70" class="lead">It's chilly outside</p>
<p v-else="tempF < 40" class="lead">It's cold outside!</p>
```

* Play with the temp to see it in action
* Add `forecastFiveDays` to the data property of the Vue instance

```js
  data: {
    cityName: 'Atlanta',
    tempF: 75,
    weatherDesc: 'Sunny',
    forecastFiveDays: []
  }
```

* Update the constants

```js
var OWM_CURRENT_URL = "api.openweathermap.org/data/2.5/weather";
var OWM_FORECAST_URL = "api.openweathermap.org/data/2.5/forecast";
var OWM_API_KEY = "4dcdc5ef8f4820617031f0658196dcba";
```

* Move the API calls into methods

```js
var app = new Vue({
  el: "#app",
  data: {
    cityName: "Atlanta",
    tempF: 75,
    weatherDesc: "Sunny",
    forecastFiveDays: []
  },
  created() {
    this.fetchCurrentWeather().then(() => this.fetchFiveDayForecast());
  },
  methods: {
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
  }
});
```

* Update the weather card (replace the whole `section`)

```html
<section id="app" class="container">
  <div class="card">
    <div class="card-body">
      <h5 class="card-title">{{ cityName }}</h5>
      <h6 class="card-subtitle mb-2 text-muted">Now: {{ tempF }}&deg; - {{ weatherDesc }}</h6>
      <p class="card-text">
        <p>Five-day Forecast</p>
        <!-- Five day forecast goes here -->
      </p>
    </div>
  </div>
</section>
```

* Demonstrate how the `v-for` directive works

```html
<p v-for="forecast in forecastFiveDays">
  <b>{{ forecast.temp }}&deg;</b>
  <br />
  <em>{{ forecast.weatherDesc }}</em>
  <br />
  <small>{{ forecast.timestamp }}</small>
</p>
```

* Add a placeholder to display the average across five days

```html
<p>Five-day Forecast (avg: {{ fiveDayAverageTemp }}&deg;)<p>
```

* Then add a computed property

```js
var app = new Vue({
  computed: {
    fiveDayAverageTemp: function() {
      return Math.round(
        this.forecastFiveDays.reduce((acc, curr) => acc + curr.temp, 0) /
          this.forecastFiveDays.length
      );
    }
  }
});
```
