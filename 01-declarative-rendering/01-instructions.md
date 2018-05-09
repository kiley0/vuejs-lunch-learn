# Vue Lunch & Learn

## Part 01 - Declarative Rendering

### Instructions

* Create a file called `index.html`
* Copy in basic HTML template with Bootstrap CSS

```html
<!doctype html>
<html lang="en">

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

  <!-- Bootstrap CSS -->
  <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.1/css/bootstrap.min.css" integrity="sha384-WskhaSGFgHYWDcbwN70/dfYBj47jz9qbsMId/iRN3ewGhXQFZCSftd1LZCfmhktB"
    crossorigin="anonymous">

  <title>Vue Weather</title>
</head>

<body>
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

  </main>

  <!-- Vue development version goes here -->
</body>

</html>
```

* Open the `index.html` in a web browser
* Include Vue from a CDN just before closing body tag

```html
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

* Below "Atlanta" add the following `section`

```html
<section id="app" class="container">
  <div class="card">
    <div class="card-body">
      <h5 class="card-title">Atlanta</h5>
      <h6 class="card-subtitle mb-2 text-muted">Sunny</h6>
      <p class="card-text">Temperature: 90&deg;</p>
    </div>
  </div>
</section>
```

* Write the following code in a new `<script>` tag below Vue

```html
<script>
  var app = new Vue({
    el: '#app',
    data: {
      cityName: 'Atlanta',
      tempF: 75,
      weatherDesc: 'Sunny'
    }
  })
</script>
```

* Update the `section` by replacing hardcoded data with `{{ variablesGoHere }}`

> At the core of Vue.js is a system that enables us to declaratively render data to the DOM using straightforward template syntax.

> The template syntax should look familar to any of our Angular developers.

> The data and the DOM are now linked, and everything is now reactive.

* In the browser console, write `app.tempF = 42` and see the value change in the dom

#### Pull the data from a real API

* Move the index file into a folder and open it in VSCode

(skip the server, it's not necessary)

<!--
* run `npm init`

* install HTTP Server
  `npm install http-server`

* start the server
  `http-server` -->

* Pull the data from a real API (OpenWeatherMap)
  `http://api.openweathermap.org/data/2.5/forecast`

* Add a `created` property to the Vue instance

```js
var OWM_BASE_URL = "api.openweathermap.org/data/2.5/weather";
var OWM_API_KEY = "4dcdc5ef8f4820617031f0658196dcba";

var app = new Vue({
  created() {
    fetch(
      `http://${OWM_BASE_URL}?q=${
        this.cityName
      }&units=imperial&APPID=${OWM_API_KEY}`
    )
      .then(response => response.json())
      .then(data => {
        if (data.cod == 200 && data.main) {
          this.tempF = data.main.temp;
          this.weatherDesc = data.weather[0].description;
        }
        console.log("Fetched weather from OpenWeatherMap:");
        console.log(data);
      })
      .catch(err => {
        console.warn(err);
      });
  }
});
```

* Refresh to see the real temperature
