## Problem

You want to write tests where user interactions come into play.

## Solution

Create an instance of the view, use jasmine-ajax to respond to network requests, then use jQuery to trigger various events. Write tests in such a way that someone who does not program can read them and verify that they are true.

## Details

When writing tests for an interface, you're not only writing them for other developers, but also designers and QA and anyone else who works with the user-facing part of the site. Write your tests for this broader audience.

Nest your tests such that the tree of possibilities is represented, and the beforeEach calls build on each other. In the example below, the 'submit form' suite branches into 'submit fails' and 'submit succeeds' branches, but all their tests include the view initialization and loading code.

In general, `beforeEach` should match `describe`, and `it`'s logic matches `it`'s test name. Again, in the example below, each `beforeEach` builds the context `describe` describes.

## Example

### FooView.coffee
```coffeescript
class FooView extends RootView
  template: require 'templates/foo-view'
  id: 'foo-view'

  events:
    'submit form': 'onSubmitForm'

  initialize: ->
    @bar = new Bar()
    @bar.fetch()

  onSubmitForm: (e) ->
    e.preventDefault()
    form = $('form')
    @bar.set(forms.formToObject(form))
    @bar.save()
```

### FooView.spec.coffee
```coffeescript
FooView = require 'views/FooView'
describe 'FooView', ->
  view = null

  beforeEach ->
    # All tests start with view initialized and @bar loaded.
    view = new FooView()
    expect(jasmine.Ajax.requests.count()).toBe(1)
    jasmine.Ajax.requests.mostRecent().respondWith({status: 200, responseText: '{_id: "abc"}'})
  
  describe 'submit form', ->
    it 'saves bar', ->
      view.$('input[name="field"]').val('Dummy data')
      view.$('form').submit()
      expect(jasmine.Ajax.requests.mostRecent().url).toBe('/db/foo')
      expect(view.$('button').attr('disabled')).toBe(true)

    describe 'submit fails', ->
      beforeEach ->
        jasmine.Ajax.requests.mostRecent().respondWith({status: 500, responseText: '{errorName: "Server Error"}'})

      ...

    describe 'submit succeeds', ->
      beforeEach ->
        jasmine.Ajax.requests.mostRecent().respondWith({status: 200, responseText: '{_id: "abc"}'})

      ...
      
```