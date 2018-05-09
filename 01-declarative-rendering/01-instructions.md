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

  <title>Learn Vue.js</title>
</head>

<body>
  <header>
    <div class="navbar navbar-dark bg-dark box-shadow">
      <div class="container d-flex justify-content-between">
        <a href="#" class="navbar-brand d-flex align-items-center">
          <strong>Learn Vue.js</strong>
        </a>
      </div>
    </div>
  </header>

  <main role="main">

    <section class="jumbotron text-center">
      <div class="container">
        <h1 class="jumbotron-heading">Learn Vue.js</h1>
        <p class="lead text-muted">By Kiley Dorton</p>
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

* Below "by Kiley Dorton" add the following `div`

```html
<div id="app">
  <p class="lead text-muted">Current Temp: 0&deg;</p>
</div>
```

* Write the following code in a new `<script>` tag below Vue

```html
<script>
  var app = new Vue({
    el: '#app',
    data: {
      tempF: 75
    }
  })
</script>
```

* Update the `div` by replacing `0` with `{{ tempF }}`

> At the core of Vue.js is a system that enables us to declaratively render data to the DOM using straightforward template syntax.

> The template syntax should look familar to any of our Angular developers.

> The data and the DOM are now linked, and everything is now reactive.

* In the browser console, write `app.tempF = 42` and see the value change in the dom
