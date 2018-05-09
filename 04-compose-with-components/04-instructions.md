# Vue Lunch & Learn

## Part 04 - Compose with Components

### Instructions

* Continue editing `index.html`

> The component system is another important concept in Vue, because it’s an abstraction that allows us to build large-scale applications composed of small, self-contained, and often reusable components. If we think about it, almost any type of application interface can be abstracted into a tree of components.

> In Vue, a component is essentially a Vue instance with pre-defined options. Registering a component in Vue is straightforward.

* Add the following to the top of the script tag:

```js
Vue.component("city-card", {
  template: "<div>I am a city card</div>"
});
```

* Then add `<city-card></city-card>` below the show/hide cities button

* Show that the div is displaying

* Now update the component with props and card markup

```js
Vue.component("city-card", {
  // The city-card component now accepts a
  // "prop", which is like a custom attribute.
  // This prop is called todo.
  props: ["city"],
  template: `
    <div class="card">
      <div class="card-body">
        {{ city.name }}
      </div>
    </div>
  `
});
```

* Now update the `<city-card></city-card>`

```html
<city-card
  v-for="city in cities"
  v-bind:city="city"
  v-bind:key="city.name">
</city-card>
```
