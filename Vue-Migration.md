Wondering how to do something with Vue instead of with Backbone? Here's the cheat sheet for you!

## Me (and other global objects) - Vuex Store

Instead of a global `me` object, use the [Vuex](https://vuex.vuejs.org/en/intro.html) `me` [module](https://vuex.vuejs.org/en/modules.html), with its logged-in-user specific [getters](https://vuex.vuejs.org/en/getters.html) and [actions](https://vuex.vuejs.org/en/actions.html).

```coffeescript
me.get('name')          ->  store.state.me.name
me.isAdmin()            ->  store.getters['me/isAdmin']
me.sendRecoveryEmail()  ->  store.dispatch('me/sendRecoveryEmail')
```

Note that in the context of components, you'll have [helpers](https://vuex.vuejs.org/en/api.html#component-binding-helpers) like `mapState`, `mapGetters`, etc, so each call doesn't have to be so long.

```coffeescript
MyComponent = {
  state: Vuex.mapState('me', ['name']),
  template:' {{ name }}' # renders to what is currently me.name in the "me" store module
}
```

While both systems are in use, changes to `me` User automatically get pushed to `me` store module. New or changed logic, even in backbone views, can use the store to speed migration. Actions and mutations on the user module should update the `me` global object until it's fully deprecated, to keep them in sync.

Other globals, such as `features` and `serverConfig` can also be added to the global vuex store, either at the root level or as their own modules, as needed.

## Using Router for Vue components

In order to use Vue Components directly in the backbone router, the first step is to import the vue component in `dynamicRequire.js`. Then add its route in the `Router.coffee`, and call `routeDirectly` with the options containing `vueRoute = true`. Also send `propsData` and `baseTemplate` in the options if required.

Example:

```javascript
//dynamicRequire.js
'views/MyVueComponent': function () { return import(/* webpackChunkName: "VueComponentExample" */ 'views/MyVueComponent')
```

Then set up the route for `MyVueComponent` in `Router.coffee`

```coffeescript
'MyVueComponentRoute(/:id)': (id) ->
  props = {
    id: parseInt(id)
  }
  # Send vueRoute: true, propsData, and baseTemplate 
  @routeDirectly('MyVueComponent', [], {propsData: props, baseTemplate: 'base-empty', vueRoute: true})
```

This will use the generic backbone view `VueComponentView.js` in the background which would render your vue component `MyVueComponent`. 

The value for `baseTemplate` will be used as a base template for the backbone view. By default, it will use `base-flat.jade` as the base template. Possible values for `baseTemplate`:
  1. base-empty : This is the empty base template without headers and footers.
  2. base-flat-empty : This is the empty base template with flat styling.
  3. base : This is the base template with coco headers and footers.
  4. base-flat (default value): This is the base template including headers and footers with flat styling.

`MyVueComponent.vue` should be created as a [single-file vue component](https://vuejs.org/v2/guide/single-file-components.html). If required, you can dynamically add a vuex module definition for your page using `this.$store.registerModule`. Make sure to also unregister it in the vue component when no longer needed, which would clear all its data.

Example:

```javascript
beforeCreate() {
    // Register a vuex store module for this page, and destroy it when navigating away
    this.$store.registerModule('MyPageModule', {
      namespaced: true,  // module will be namespaced to 'MyPageModule/'
      state: {
        myState: 'demoValue'
      }
      ...
    })
  }

destroyed() {
    // Destroy the dynamically registered module for this page by unregistering it
    this.$store.unregisterModule('MyPageModule')
  }

//Use the registered module as a computed property in the vue component
computed: Vuex.mapState('MyVuexModule', ['testState']) //this means this.testState = store.state.MyVuexModule.testState
```

## RootView -> RootComponent

NOTE: This is another way of routing to vue components using the backbone router. However using this method, you will not be able to use vue components directly in the router, and will have to create a new backbone view with each vue component and then use the router as-is. This is NOT RECOMMENDED, since we are moving towards full VueJS migration and eventually want to deprecate `RootComponent.coffee` going forward. 

In order to route using this method, you will need to use a RootComponent as a wrapper for your component, i.e. create a backbone view extending from `RootComponent`. Give it a single root Vue component and, if needed, a vuex store module which will be dynamically added as the 'page' module upon navigating to the page and will be removed by the RootComponent when navigating away.

Backbone:

```coffeescript
RootView = require 'views/core/RootView'
module.exports = class MyView extends RootView
  ...
```

Vue:

```coffeescript
RootComponent = require 'views/core/RootComponent'

MyComponent = Vue.extend
  ...

module.exports = class MyView extends RootComponent
  VueComponent: MyComponent
  vuexModule: -> {
    namespaced: true # module will be namespaced to 'page/'
    ...
  }
  ...
```

## Page Layout for Vue Components

Instead of extending `base.jade` and `base-flat.jade`, include the `page-layout` component and put content inside it.

With Backbone:

```coffeescript
# View
RootView = require 'views/core/RootView'
class MyView extends RootView
  template: require('templates/my-view')
```

```jade
// Template
extends /templates/base-flat

block content
  div Content...
```

With Vue:

```
# Component
<template lang="pug">
flat-layout
  div Content...
</template>

<script>
import FlatLayout from 'core/components/FlatLayout'
module.exports = Vue.extend
  components:
    'flat-layout': FlatLayout
</script>
```

This setup uses [Vue.js slots](https://vuejs.org/v2/guide/components.html#Content-Distribution-with-Slots).

## Using Isolated Vue components

In order to use other isolated Vue components inside your vue component, include it in the components and use it in the template.

```
# Component
<template lang="pug">
pie-chart(
    :percent='10',
    :stroke-width="10",
    color="#20572B",
    :opacity="1"
  )
</template>

<script>
import PieChart from 'core/components/PieComponent'
module.exports = Vue.extend
  components:
    'pie-chart': PieChart
</script>
```


## Internal vue components in existing Backbone Views

Say you want to take a smaller piece of a Backbone view and make it a Vue component. To do this, create (or update) the vue component instance in the Backbone view's `afterRender` method, and destroy it in the view's `destroy` method.

```coffeescript
module.exports = class MyView extends CocoView
  afterRender: ->
    if @myComponent
      @$el.find('#target').replaceWith(@myComponent.$el)
    else
      @myComponent = new MyComponent({
        el: @$el.find('#target')[0]
      })
    super(arguments...)

  destroy: ->
    @myComponent.$destroy()
```

To share data between Backbone and vue components, the Backbone view can:

* grab data through the vuex store object (`require('core/store')`)
* set the vue component's [$data](https://vuejs.org/v2/api/#vm-data)
* listen to vue component changes with [$watch](https://vuejs.org/v2/api/#vm-watch)

## Network Requests

Instead of using `$.ajax` or Backbone model/collection methods, call `api` functions which are wrapped around the [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API).

```coffeescript
# Backbone Collections/Models
Users = require('collections/Users')
users = new Users()
jqxhr = users.fetch({data: {project:'name'}})
jqxhr.done (rawResponse) -> ...

# Fetch API
api = require('core/api')
promise = api.users.fetch({data: {project:'name'}})
promise.then (rawResponse) -> ...
```

Network errors generated by the API are rejected as objects in the promise. These objects all at least have `message` and `code` properties.

## Page Errors

One of the things the SuperModel does is handle page load errors, re-rendering the page with a generic load error if a necessary resource fails to load. So if you try to go to a classroom page where you don't have access to the page, the SuperModel shows a "Forbidden" error. The PageLayout component can do this as well. However, it's explicit instead of automatic, and it's more easily customizable.

```coffeescript
# SuperModel
users = new Users()
@supermodel.trackRequest(users.fetch()) # shows an error if this resource fails to load
...

# Vue
api.users.fetch({data: {project:'name'}})
.then (users) ->
  ...
.catch (e) ->
  @$store.commit('addPageError', e)
```

This appends the error to a list of errors in the global store, and the PageLayout is set to show the PageErrors component instead of the page content if there are errors. But you can handle these errors however you like for any given page, either by using a different layout component, or doing something else within the `catch`. If network errors are not caught, they show up the same way as they do now: as noty's when in development or logged in as an admin.

## Page Load Progress
There is no generic system for tracking page-load progress to replace the SuperModel. Instead, try using the FontAwesome spinner.

```coffeescript
# Component
MyComponent = Vue.extend
  data: -> {
    loading: true # have a bootstrap progress bar width keyed off this
  }
  created: ->
    p1 = api.thing.fetch()
    p2 = api.otherThing.fetch()
    Promise.all([p1,p2]).then ([res1, res2]) =>
      this.loading = false
```

```jade
// Template
div
  i.fa.fa-spinner.fa-spin.fa-3x(v-if="loading")
  div(v-else) Content...
```

## Bootstrap

Bootstrap components can generally be used the same as they are now. For example, a [modal with a trigger button](http://getbootstrap.com/javascript/#live-demo) will still work if put into Vue. But it's preferable to store all vue component state in the vue component. So with tabs, instead of using [JavaScript to trigger switching between them](http://getbootstrap.com/javascript/#tabs), key the tab [active class](http://getbootstrap.com/components/#nav-tabs) off the component state and set up logic to change the state when a tab is clicked.

```jade
ul.nav.nav-tabs
  li(v-bind:class="{active: tab === 'home' }" click="setTab('home')") Home
  li(v-bind:class="{active: tab === 'profile' }" click="setTab('profile')") Profile
  li(v-bind:class="{active: tab === 'messages' }" click="setTab('messages')") Messages
```

## Handy Tools

Install the [Vue.js Devtools Chrome Extension](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd?hl=en). Use it to see what components are on the page and the state of the vuex store.

## File Structure

Where to find/put all these new files?

```
/app
  /core
    /api
      fetch-json.coffee: improved Fetch API function
      index.coffee: puts all the other modules in this folder together, makes it possible to require('/core/api')
      <collection>.coffee: all network endpoints for this collection

    /core
      /components: all non-root-level, common components

    /store
      /modules
        me.coffee: Replacement to global "me"
      index.coffee: Where all the global store pieces and modules are put together. Might get broken down later.

    /templates: where all component templates go

    /views: where all root-level components go
      /core
        RootComponent.coffee: shims page-level components to the Router
```

## Translations

Instead of passing data through `data-i18n` parameters, call the `i18n.t` function directly through `$t`. It's also available on the vue component instance as `@$t`.

```jade
div(data-i18n="some.key") // with Backbone

div {{ $t("some.key") }} // with Vue
```

## window.currentView -> window.rootComponent

RootComponent will put its vue component in the global namespace as `rootComponent` to aid development. Don't use this in code, though! A component can access its root component with `@$root`, but as much as possible use the Vuex store to communicate between disparate pieces of logic.