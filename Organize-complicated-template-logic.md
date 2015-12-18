## Problem

A template is overly complicated.

## Solutions

* Delegate complicated logic to views, models or collections, accessed through the template's `view` property.
* Break down the template into [jade mixins](http://jade-lang.com/reference/mixins/).
* Break down the view into subviews.

## Details

Jade templates can run any sort of JavaScript logic, but that doesn't mean they should. Templates should minimize logic and focus on layout and presentation. If a template is getting to be too large to really dig into, consider these options:

### Shunt Logic To Views, Models, Collections

Say every time you render a view, you need a particular model from a collection, but you need complicated logic to find that model. Add a function to the view which the template can call to get that model.

*FooView.coffee*

  ```coffeescript
  RootView = require 'views/core/RootView'
  template = require 'templates/foo-view'
  Foos = require 'collections/Foos'
  Users = require 'collections/Users'
  
  module.exports = class FooView extends RootView
    id: 'foo-view'
    template: template
    initialize: ->
      @foos = new Foos()
      @users = new Users()
      ...

    findThatFooFor: (user) ->
      madFilterFunc = (foo) ->
        # ... lines and lines of mad code
      return @foos.find(madFilterFunc)
  ```

*foo-view.jade*

  ```jade
  extends /templates/base

  block content
    h1 Users
    li
      for user in users
        - var foo = view.findThatFooFor(user)
        ul #{user.get('name')}'s Foo: #{foo.get('name')}.
  ```

If the shunted logic would be helpful throughout the client, it should instead be added to the Model or Collection class.

### Jade Mixins

Jade templates can get rather deep, and at some point it's hard to figure out what indent ends where, or what's going on overall. Break the template into middleware chunks so that the overall structure and individual parts can be more easily grocked, in the same way and for the same reason that you'd break a large function into smaller functions. See [jade's documentation on mixins](http://jade-lang.com/reference/mixins/) for implementation details and examples.

### SubViews

Particularly complicated views should be broken down into subviews. This is the solution with the highest overhead, so it should not be chosen lightly.

## Resources

* [Jade Mixins](http://jade-lang.com/reference/mixins/)