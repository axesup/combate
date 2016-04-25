## Problem

You want the website to use a collection which has been set up on the server.

## Solution

Create a Backbone Model in `/app/models` and a Collection in `/app/collections` to be used imported and used by any View. Use CodeCombat's subclasses, CocoModel and CocoCollection.

## Example

If your new collection has endpoints at `/db/widgets`, the Model and Collection files would look like this:

**/app/models/Widget.coffee**
```coffeescript
CocoModel = require './CocoModel'
schema = require 'schemas/models/widget.schema'

module.exports = class Widget extends CocoModel
  @className: 'Widget'
  @schema: schema
  urlRoot: '/db/widgets'
```

**/app/collections/Widgets.coffee**
```coffeescript
Widget = require 'models/Widget'
CocoCollection = require 'collections/CocoCollection'

module.exports = class Widgets extends CocoCollection
  model: Widget
  url: '/db/widgets'
```

Then you will be able to use Backbone to access and manipulate data in that collection:

* [Model.fetch()](http://backbonejs.org/#Model-fetch)
* [Model.save()](http://backbonejs.org/#Model-save)
* [Collection.fetch()](http://backbonejs.org/#Collection-fetch)

## Resources

* [Backbone](http://backbonejs.org/)
