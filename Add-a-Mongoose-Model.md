## Problem

You want to access a database collection on the server.

## Solution

Create a Mongoose model in `/server/models`.

## Details

Mongoose is the server's interface for interacting with MongoDB. It provides functions for running standard MongoDB queries as well as many other features like Promises, middleware, plugins and property type casting.

## Example

**/server/models/SomeModel.coffee**
```coffeescript
mongoose = require 'mongoose'
plugins = require '../plugins/plugins'
jsonSchema = require '../../app/schemas/models/some-model.schema'

# 1. Make the schema. Only include properties in the schema that should be
#    cast: ObjectIds and Dates. The exhaustive schema for the documentation
#    should be the JSON schema.
SomeModelSchema = new mongoose.Schema({
  userID: mongoose.Types.ObjectId
}, {strict: false})


# 2. Install plugins. These add common schema properties, indexes and functions to the schema.
SomeModelSchema.plugin(plugins.NamedPlugin)
SomeModelSchema.plugin(plugins.SearchablePlugin, {searchable: ['name', 'description']})


# 3. Add common static properties.
#   * editableProperties: whitelist of properties that may be edited through 
#     the collection's standard PUT endpoint
#   * jsonSchema: used in POST and PUT to validate data before saving to the db
SomeModelSchema.statics.editableProperties = ['name', 'description', 'userID']
SomeModelSchema.statics.jsonSchema = jsonSchema 


# 4. Create the model from the schema and export it. The first argument should be 
#    the all-lowercase, dot-separated, singular version of the collection name. Mongoose
#    will pluralize that for the collection name.
module.exports = mongoose.model('some.model', SomeModelSchema)
```

See Mongoose's guide and API docs for more available features.

## Resources

* [Mongoose Guide](http://mongoosejs.com/docs/guide.html)
* [Mongoose API Docs](http://mongoosejs.com/docs/api.html)