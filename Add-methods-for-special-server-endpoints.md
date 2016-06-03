## Problem

You want the client to have a common way to access a server url which is not part of a standard RESTful API.

## Solution

Find (or create) the Model or Collection which is what is returned by the API. Add a function to it that takes required arguments and (lastly) jQuery options and returns the jQuery jqxhr. Use this function anywhere in the codebase this endpoint is accessed.

## Details

Backbone comes with two network calls which can be modeled after: [`fetch`](http://backbonejs.org/#Model-fetch) and [`save`](http://backbonejs.org/#Model-save). In both cases, the last argument is an `options` object which is passed through to [jQuery's ajax function](http://api.jquery.com/jquery.ajax/), and the functions return the [`jqxhr` object](http://api.jquery.com/Types/#jqXHR). All other network requests should have these same characteristics, and can often build on them, `fetch` in particular. By building on Backbone's `fetch`, the network request responses also automatically update the Model or Collection which is executing the request.

## Examples

Each of these functions:

1. Overwrites options values that are required for the endpoint.
1. Ends with a `fetch` which, in CoffeeScript, returns the result, the `jqxhr`.

### GET with special URL

```coffeescript
class Levels extends CocoCollection
  fetchForClassroom: (classroomID, options={}) ->
    options.url = "/db/classroom/#{classroomID}/levels"
    @fetch(options)
```

### GET by parameter

```coffeescript
module.exports = class Campaigns extends CocoCollection
  fetchByType: (type, options={}) ->
    options.data ?= {}
    options.data.type = type
    @fetch(options)
```

### Non-GET action for a specific document

```coffeescript
module.exports = class Classroom extends CocoModel
  removeMember: (userID, opts) ->
    options = {
      url: _.result(@, 'url') + '/members'
      type: 'DELETE'
      data: { userID: userID }
    }
    _.extend options, opts
    @fetch(options)
```