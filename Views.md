Views are extended versions of [Backbone Views](http://backbonejs.org/#View). All views should subclass CocoView and its subclasses in /app/views/kinds and generally use their features. These include:

### Events, subscriptions and shortcuts
Described in the [wiki article](https://github.com/codecombat/codecombat/wiki/Events%2C-subscriptions%2C-shortcuts).

### Subview adding

Larger views can (and should!) be broken down into many constituent parts, and in order to tie them together:

1. In the parent view template, have the id of the child view where it will be inserted.
1. In the parent view initialization logic, either in afterRender or after whatever resources are loaded, use @addSubview for a CocoView instance.

Views which have no parent should subclass RootView, and any subviews can simply subclass CocoView directly.

Using addSubview is important to do because it ties in with the next feature:

### Setup/Teardown

When a view is navigated away from, its destroy function is called, which tears down those shortcuts, subscriptions and events as best it can. It also recursively tears down any subviews that were inserted through insertSubview.

### Modals

Modals are views too, and by using openModalView in CocoView they can be handled uniformly. Modals should subclass ModalView.

### Templates

A view typically has one jade template associated with it. When you create a view in /app/views, you should also add a jade file in /app/templates, following a parallel path and named same as the view but with a hyphenated-name instead of CamelCaseName.

A template will typically look something like this:

```jade
extends /templates/base

block content
  p Main content goes here.
  p Insert static content from the view like this: #{view.modelYouLoaded.get('name')}.
  p= view.accountStatusString()
  - var now = moment(new Date());
  p It is now #{now.format('LLLL')}.
```

Every template has access to the view that renders it, as well as a handful of other globals such as lodash (_) and moment. See `getRenderData` in [CocoView.coffee](https://github.com/codecombat/codecombat/blob/master/app/views/core/CocoView.coffee) for a complete, current list. Use view to hold data and middleware you want to use for your particular view.

***

If you're building client views, it's recommended you look through the files in /app/views/kinds to familiarize yourself with the common tools, and how things are generally done.