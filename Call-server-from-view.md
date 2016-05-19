## Problem

You want to load or make changes to data stored on the server.

## Solution

Initialize the Model or Collection of the data you are loading and call the appropriate function.

## Details

Most server endpoint urls start with `/db/<collection-name>` and return either one or many of that collection. What is returned determines which Backbone Model or Collection to use. For example, if you are loading multiple Classrooms, then you should use the [Classrooms Collection](https://github.com/codecombat/codecombat/blob/master/app/collections/Classrooms.coffee).

If you are loading one of something and you have its `_id` or `slug` (such as from the URL), initialize the Model with `{_id: idOrSlug}` and `fetch` it.

```
user = new User({_id: 'mr-anderson'})
user.fetch()
```

If you are loading many of something, initialize its Backbone Collection and `fetch` it.

```
users = new Users()
users.fetch()
```

Many Models and Collections have `fetch*` functions for GET requests with special GET parameters or URLs.

```
campaigns = new Campaigns()
campaigns.fetchByType('course')
```

To save changes to a Model, use `set` and then `save`.

```
user.set('email', 'new@email.com')
user.save()
```

All of these functions need to handle network responses asynchronously. This can be done several ways, in order of recommendation:

1. If you are fetching data which the view needs before it can even properly render, give the returned value to `@supermodel.trackRequest`
1. Listen to Model or Collection [Backbone events](http://backbonejs.org/#Events-catalog)
1. Provide `success`, `error`, and `done` callbacks through the options parameter, which is passed to jQuery.ajax.
1. Use the jQuery Promise returned by the function manually. This is not currently recommended as jQuery Promises are not compliant with ES6 Promises.

```coffeescript
class SomeView extends CocoView
  initialize: ->
    user = new User({_id: someID})
  
    # 1.
    @supermodel.trackRequest(user.fetch())

    # 2a.
    user.fetch()
    @listenToOnce(user, 'sync', @doSomething)
  
    # 2b.
    user.fetch()
    user.once('sync', @doSomething, @)

    # 3
    user.fetch({ success: => @doSomething() })
  
    # 4
    user.fetch().then(=> @doSomething())
```

`@supermodel.trackRequest` has the view show a loading bar until every tracked request succeeds, at which point `onLoaded` is called, which re-renders the view. If any request fails, the view displays the first error that occurs. To handle success and errors manually for network requests that happen after page load, see [[how to add a form|add-a-form]].