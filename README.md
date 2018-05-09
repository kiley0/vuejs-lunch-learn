# vuejs-lunch-learn

Introducing Vue.js to my company

## Outline

* What is Vue.js?
* 3 minute history

* 01 - Declarative Rendering
* 02 - Conditionals and Loops
* 03 - Handle User Input
* 04 - Compose with Components
* 05 - Continuous Deployment with Netlify
* 06 - Install and use the vue-cli

* Walk through the real-world vue project

* Where to go next (nuxt)

## What is Vue.js?

> Vue (pronounced like view) is a progressive framework for building user interfaces. Unlike other monolithic frameworks, Vue is designed from the ground up to be incrementally adoptable.

> The core library is focused on the view layer only, and is easy to pick up and integrate with other libraries or existing projects. On the other hand, Vue is also perfectly capable of powering sophisticated Single-Page Applications when used in combination with modern tooling and supporting libraries.

### Comparing Vue to other Frameworks

**Vue and React**

They both:

* utilize a virtual DOM
* provide reactive and composable view components
* maintain focus in the core library, with concerns such as routing and global state management handled by companion libraries

Performance comparison of frameworks:
http://www.stefankrause.net/js-frameworks-benchmark7/table.html

Optimization efforts:

> In React, when a component’s state changes, it triggers the re-render of the entire component sub-tree, starting at that component as root. To avoid unnecessary re-renders of child components, you need to either use PureComponent or implement shouldComponentUpdate whenever you can. You may also need to use immutable data structures to make your state changes more optimization-friendly. However, in certain cases you may not be able to rely on such optimizations because PureComponent/shouldComponentUpdate assumes the entire sub tree’s render output is determined by the props of the current component. If that is not the case, then such optimizations may lead to inconsistent DOM state.

> In Vue, a component’s dependencies are automatically tracked during its render, so the system knows precisely which components actually need to re-render when state changes. Each component can be considered to have shouldComponentUpdate automatically implemented for you, without the nested component caveats.

> Overall this removes the need for a whole class of performance optimizations from the developer’s plate, and allows them to focus more on building the app itself as it scales.

> In Vue, we also have render functions and even support JSX, because sometimes you do need that power. However, as the default experience we offer templates as a simpler alternative. Any valid HTML is also a valid Vue template, and this leads to a few advantages of its own:

* For many developers who have been working with HTML, templates feel more natural to read and write. The preference itself can be somewhat subjective, but if it makes the developer more productive then the benefit is objective.

* HTML-based templates make it much easier to progressively migrate existing applications to take advantage of Vue’s reactivity features.

* It also makes it much easier for designers and less experienced developers to parse and contribute to the codebase.

**Pro tip**

> We recommend using templates for presentational components and render function / JSX for logical ones.

## Quick History

> Vue was created by Evan You after working for Google using AngularJS in a number of projects. He later summed up his thought process, "I figured, what if I could just extract the part that I really liked about Angular and build something really lightweight without all the extra concepts involved?"

> Vue was originally released in February 2014.

> Vue is supported by corporate sponsors and people like you and me. On Patreon, vue currently receives $15,857 per month
> https://www.patreon.com/evanyou

## Walk through the real-world vue project

Go here: https://github.com/gothinkster/vue-realworld-example-app
Clone locally

```
# install dependencies
> npm install
# serve with hot reload at localhost:8080
> npm run dev
```

## Where to go next

* Nuxt
  https://nuxtjs.org/guide

* Vue Roadmap
  https://github.com/vuejs/roadmap
