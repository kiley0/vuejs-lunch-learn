# Vue Lunch & Learn

## Part 03 - Handle User Input

### Instructions

* Continue editing `index.html`

> To let users interact with your app, we can use the v-on directive to attach event listeners that invoke methods on our Vue instances.

* Add a method to generate a random temperature

```js
var app = new Vue({
  methods: {
    randomizeTemp: function() {
      this.tempF = Math.floor(Math.random() * 100);
    }
  }
});
```

* Add a button to generate a random temperature

```html
<button type="button" class="btn" v-on:click="randomizeTemp">New Temp</button>
```

* Add another button

```html
<button type="button" class="btn btn-primary" v-on:click="toggleShowCities">Show Cities</button>
```

* Add a `v-if` directive to the cities div

`<div v-if="showCities">...</div>`

* Add a `showCities` boolean to the data property

```js
var app = new Vue({
  data: {
    showCities: false
  }
});
```

* Add a methods property to the Vue instance (below data)

```js
var app = new Vue({
  methods: {
    toggleShowCities: function () {
      this.showCities = !this.showCities
    }
  }
)}
```

* Update the button text

`{{showCities ? 'Hide' : 'Show'}}`
