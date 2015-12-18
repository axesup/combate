## Problem

You want to access parts of a URL for your view, for example to view a specific document in the db.

## Solution

For path parameters, use [Backbone Router routes](http://backbonejs.org/#Router-routes) in the url you add to [Router.coffee](https://github.com/codecombat/codecombat/blob/master/app/core/Router.coffee), and access the values in your view's [initialize](http://backbonejs.org/#View-constructor) function. For GET parameters, use [core/utils.coffee](https://github.com/codecombat/codecombat/blob/master/app/core/utils.coffee)'s `getQueryVariable` function.

## Example

In *Router.coffee*

  ```coffeescript
  routes:
    '/doodads/:doodadID': go('DoodadView')
    ...
  ```

*DoodadView.coffee*

  ```coffee
  utils = require 'core/utils'

  class DoodadView extends RootView
    initialize: (options, doodadID) ->
      @doodad = new Doodad({_id: doodadID})
      @showTab = utils.getQueryVariable('show-tab')
  ```

So for example when navigating to the url `/doodad/sprocket?show-tab=change-history`, `doodadID` will be `"sprocket"` and `@showTab` will be `"change-history"`.

## Resources

* [Backbone Router routes](http://backbonejs.org/#Router-routes)