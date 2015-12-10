## Problem

You want to create a new page on the CodeCombat website.

## Solution

Create view, template, and style files and then tie the url to the view in the Router.

## Details

First, create the three core files:

1. **View file**. In [/app/views](https://github.com/codecombat/codecombat/tree/master/app/views) or one of the subfolders, create the view file. The name should be CamelCase, end with 'View', and be a CoffeeScript file. The contents should be something like this:

  ```coffeescript
  RootView = require 'views/core/RootView'
  template = require 'templates/foo-view'
  
  module.exports = class FooView extends RootView
    id: 'foo-view'
    template: template
  ```
1. **Template file**. In [/app/templates](https://github.com/codecombat/codecombat/tree/master/app/templates), or one of the subfolders, create the template file. The name should be hyphenated, end with '-view', and be a jade file, and the subfolder-path should match the View's. The contents should look something like this:

  ```jade
  extends /templates/base

  block content
    p Hello World
  ```

1. **Stylesheet (optional)**. In [/app/styles](https://github.com/codecombat/codecombat/tree/master/app/styles), or one of the subfolders, create the stylesheet file. The name should be hyphenated, end with '-view', be a sass file, and the subfolder-path should match the View's. The contents should look something like this:

  ```sass
  #foo-view
    color: black
  ```

Once the files are created, add the route to [/app/core/Router.coffee](https://github.com/codecombat/codecombat/blob/master/app/core/Router.coffee). Use the `go` function to wrap around the path to the view file.

You should now be able to navigate to your new route and view your new view.

## Resources
* [Backbone](http://backbonejs.org)
* [CoffeeScript] (http://coffeescript.org/)
* [Jade](http://jade-lang.com/)
* [Sass](http://sass-lang.com/documentation/file.SASS_REFERENCE.html)