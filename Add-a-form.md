## Problem
You want to add a form to a view.

## Solution
Use Bootstrap forms to lay out the form, the [core/forms module](https://github.com/codecombat/codecombat/blob/master/app/core/forms.coffee) to get the data from the form, tv4 and the forms module to validate the form, and Backbone to submit the data.

## Details
See the [Bootstrap Forms documentation](http://getbootstrap.com/css/#forms). Unless otherwise noted, create forms according to Bootstrap's instructions, and follow good forms best practices, such as setting tabindex, [type](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms/How_to_structure_an_HTML_form#The_<input>_element), [aria and role](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms/How_to_structure_an_HTML_form#Using_ARIA_to_structure_HTML_forms) attributes.

### Form submission
Forms are submitted over AJAX, but by default they perform browser submissions when submitted. Use Backbone events to override this behavior.

```coffeescript
events:
  'submit form': 'onSubmitForm'

onSubmitForm: (e) ->
  e.preventDefault()
  ...
```

Remember that button elements without a type will submit forms by default. Set their type to 'button' to prevent this.

[Example](https://github.com/codecombat/codecombat/blob/5fffb2eefb80f6fb11a8dfcb9bb227eae611cb9f/app/views/RequestQuoteView.coffee#L49)

### Getting Data
Every input field's name attribute should be its JSON property name. Then use the forms.formToObject to create a JSON object from the form, where the keys are the name fields. You may need to massage the data at that point.

```jade
form
  .form-group
    label Name
    input(name="name")
```

```coffeescript
forms = require 'core/forms'
forms.formToObject($('form')) # returns { name: 'Whatever is in the input' }
```

[Example](https://github.com/codecombat/codecombat/blob/5fffb2eefb80f6fb11a8dfcb9bb227eae611cb9f/app/views/RequestQuoteView.coffee#L51-L53)

### Validating Data
When possible, data should be validated before submitting to the server. Use TV4 and json-schema in conjunction with the forms library to do the basics like what fields are required. If the data is being saved to a Model with an existing json schema, you can call the model's validate function. If there are errors, use forms.applyErrorsToForm. For custom error messages, use forms.applyErrorToProperty. Use forms.clearFormAlerts whenever retrying so that errors do not accumulate.

```coffeescript
jsonSchema = {
  type: 'object'
  required: ['name']
  properties: {
    name: { type: 'string' }
  }
}

form = $('form')
forms.clearFormAlerts(form) # Removes any previous errors showing
attrs = forms.formToObject()
result = tv4.validateMultiple(attrs, jsonSchema)
if not result.valid
  # shows "Required" error by name field if the field is empty
  return forms.applyErrorsToForm(form, result.errors)
if attrs.name.length is 42
  # arbitrary custom error handling
  return forms.setErrorToProperty(form, 'name', 'Names cannot be 42 characters long')
  
```

[Example](https://github.com/codecombat/codecombat/blob/5fffb2eefb80f6fb11a8dfcb9bb227eae611cb9f/app/views/RequestQuoteView.coffee#L54-L61)

### Submitting Data
Data should be submitted through Backbone Models. Either use an existing Model or create one specifically for the task. When submitting data, disable the submit button and set its text to something appropriate like 'saving' or 'sending'. How the form handles a successful submission depends on the form, but a good rule of thumb is to show a success alert above the submit button. And if the form should generally not be resubmitted (like a contact form), keep the submit button disabled unless the form changes.

```coffeescript
attrs = forms.formToObject(form)
# perform validation
clan = new Clan(attrs)
button = $('button[type="submit"]')
button.text('Sending').attr('disabled', true)
clan.save()
clan.on 'sync', ->
  $('#success-alert').removeClass('hide')
  button.text('Submit').attr('disabled', false)

clan.on 'error', ->
  button.text('Submit').attr('disabled', false)
```

[Example]
(https://github.com/codecombat/codecombat/blob/5fffb2eefb80f6fb11a8dfcb9bb227eae611cb9f/app/views/RequestQuoteView.coffee#L62-L75)

When in game, play a sound on submission. [Example](https://github.com/codecombat/codecombat/blob/master/app/views/play/level/modal/ReloadLevelModal.coffee#L12)

## Resources
* [Bootstrap Forms](http://getbootstrap.com/css/#forms)
* [forms module](https://github.com/codecombat/codecombat/blob/master/app/core/forms.coffee)
* [How to structure an HTML form (MDN)](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms/How_to_structure_an_HTML_form)
* [Backbone Model](http://backbonejs.org/#Model)
* [json-schema.org](http://json-schema.org/)
* [TV4](https://github.com/geraintluff/tv4)
