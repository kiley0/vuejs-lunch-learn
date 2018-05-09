# Vue Lunch & Learn

## Part 04 - Compose with Components

### Instructions

* Continue editing `index.html`

> The component system is another important concept in Vue, because it’s an abstraction that allows us to build large-scale applications composed of small, self-contained, and often reusable components. If we think about it, almost any type of application interface can be abstracted into a tree of components.

> In Vue, a component is essentially a Vue instance with pre-defined options. Registering a component in Vue is straightforward.

* Add the following to the top of the script tag:

```js
Vue.component("city-card", {
  template: `<h1>City Card <span class="badge badge-secondary">New</span></h1>`
});
```

* Then add `<city-card></city-card>` below the select

* Show that the component is displaying

* Now update the component with props and card markup

```js
Vue.component("city-card", {
  // The city-card component now accepts a
  // "prop", which is like a custom attribute.
  props: [
    "cityName",
    "tempF",
    "weatherDesc",
    "fiveDayAverageTemp",
    "forecastFiveDays"
  ],
  template: `
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
  `
});
```

* Now update the `<city-card></city-card>`

```html
      <city-card :city-name="cityName" :temp-f="tempF" :weather-desc="weatherDesc" :five-day-average-temp="fiveDayAverageTemp"
        :forecast-five-days="forecastFiveDays"></city-card>
```

* And move over the state for the show/hide of forecast

```js
      data: function () {
        return {
          showForecast: false,
        }
      },
      methods: {
        toggleForecast: function () {
          this.showForecast = !this.showForecast
        },
      }
```
