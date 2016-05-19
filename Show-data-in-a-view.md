## Problem

You want to display data loaded in your view in the view's template.

## Solution

Access any properties in the template's view with the `view` property.

## Details

As long as the view subclasses CocoView or one of its subclasses (RootView, ModalView, etc), the template is rendered with a common context. This context always includes a `view` property, which provides access to, for example, models and collections loaded by the view.

## Examples

*FooView.coffee*

  ```coffee
  RootView = require 'views/core/RootView'
  Foos = require 'collections/Foos'
  utils = require 'core/utils'

  class FoosView extends RootView
    template: require 'templates/foos-view'
    initialize: (options, doodadID) ->
      @foos = new Foos()
      @supermodel.trackRequest(@foos.fetchForDoodad(doodadID))
  ```

*foos-view.jade*

  ```jade
  extends /templates/base

  block content
    h1 All the Foos
    ul
      for foo in view.foos.models
        li= foo.get('name')

    h1 Foos Where Bar Is True
    ul
      for foo in view.foos.where({bar: true})
        li= foo.get('name')
  ```