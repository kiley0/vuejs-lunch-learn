# Vue Lunch & Learn

## Part 03 - Handle User Input

### Instructions

* Continue editing `index.html`

> To let users interact with your app, we can use the v-on directive to attach event listeners that invoke methods on our Vue instances.

* Add button to toggle the forecast

```html
<button type="button" class="btn btn-primary" v-on:click="toggleForecast">Show Forecast</button>
```

* Add a `v-if` directive to a `div` around the forecast

`<div v-if="showForecast">...</div>`

* Add a `showForecast` boolean to the data property

```js
var app = new Vue({
  data: {
    showForecast: false
  }
});
```

* Add a methods property to the Vue instance (below data)

```js
var app = new Vue({
  methods: {
    toggleForecast: function () {
      this.showForecast = !this.showForecast
    }
  }
)}
```

* Update the button text

`{{showForecast ? 'Hide' : 'Show'}}`

#### Two-way data binding

* Add a select above the card

```html
  <div class="form-group mb-4">
    <label for="citySelect">Select a city</label>
    <select class="form-control" id="citySelect">
      <option>Atlanta</option>
      <option>London</option>
      <option>Tokyo</option>
      <option>San Francisco</option>
      <option>Cairo</option>
    </select>
  </div>
```

* Add the `v-model="cityName"` directive to the select
* Demonstrate two-way data binding

* Notice the data is not changing, then add `v-on:change="fetchData"`

```js
  fetchData: function () {
    return this.fetchCurrentWeather()
      .then(() => this.fetchFiveDayForecast());
  },
```

* Demonstrate that the two-way binding is still working
