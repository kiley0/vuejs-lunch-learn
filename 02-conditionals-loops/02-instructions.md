# Vue Lunch & Learn

## Part 02 - Conditionals and Loops

### Instructions

* Continue editing `index.html`
* Add a few `p` tags below the current temp

```html
<p v-if="tempF >= 90" class="lead text-muted">It's hot outside!</p>
```

* Change the temp in the console and show v-if directive working
* Add the following below the first v-if

```html
<p v-else-if="tempF >= 80 && tempF < 90" class="lead text-muted">It's warm outside</p>
<p v-else-if="tempF >= 70 && tempF < 80" class="lead text-muted">It's comfortable outside</p>
<p v-else-if="tempF >= 40 && tempF < 70" class="lead text-muted">It's chilly outside</p>
<p v-else="tempF < 40" class="lead text-muted">It's cold outside!</p>
```

* Play with the temp to see it in action
* Add the following to the data property of the Vue instance

```js
  data: {
    tempF: 75,
    cities: [
      {
        name: 'Atlanta',
        tempF: 75
      },
      {
        name: 'New York',
        tempF: 65
      },
      {
        name: 'Austin',
        tempF: 85
      },
    ]
  }
```

* Add city cards below the temperature

```html
<div>
  <div class="card" v-for="city in cities">
    <div class="card-body">
      {{ city.name }} - {{ city.tempF }}&deg;
    </div>
  </div>
</div>
```

* Demonstrate how the `v-for` directive works
* In the console, `app.cities.push({name: "San Francisco"})`
