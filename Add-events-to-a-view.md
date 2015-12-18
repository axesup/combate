## Problem

You want your view to do something when the user clicks or otherwise fires a JavaScript/jQuery event.

## Solution

Add or extend [Backbone.View's events property](http://backbonejs.org/#View-events). Be sure to follow [CodeCombat's event naming guidelines](https://github.com/codecombat/codecombat/wiki/Events%2C-subscriptions%2C-shortcuts#events).

## Example

*FooView.coffee*

  ```coffeescript
  CocoView = require 'views/core/CocoView'
  template = require 'templates/foo-view'
  
  module.exports = class FooView extends CocoView
    id: 'foo-view'
    template: template
    events:
      'click #some-btn': 'onClickSomeButton'

    onClickSomeButton: (e) ->
      console.log('Some button was clicked', e);
  ```

*foo-view.jade*

  ```jade
  button#some-btn.btn.btn-default Click Me!
  ```

## Resources

* [Backbone.View events](http://backbonejs.org/#View-events)
* [jQuery event object](https://api.jquery.com/category/events/event-object/)
* [[Events, subscriptions, shortcuts]]