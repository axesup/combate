## Problem

You want to set up a page for translation.

## Solution

Within Jade, add the attribute `data-i18n` to the element to set its text. The value of the attribute should point to a string in `/app/locale/en.coffee`. To set the translated string to an attribute instead of the element's text value, preface the string with the attribute name in brackets. Within CoffeeScript, use `$.i18n.t()`. Mark sections of templates that are not to be translated with DNT.

## Details

All static strings to be translated are kept in [/app/locale/en.coffee](https://github.com/codecombat/codecombat/blob/master/app/locale/en.coffee). When a jade template is rendered by a CocoView, it finds all elements with the attribute `data-i18n`, and based on the user's language settings, takes strings from the locale folder for that key. Strings that are not translated default to the English translation. We use a forked version of [i18next](http://i18next.com/).

## Examples

### en.coffee

```coffeescripts
module.exports = 
  common:
    info: "Information"
    enter_name: "Enter name here"
    send: "Send"
    sending: "Sending"
```

### Jade file
```jade
h1(data-i18n="common.info") // Will display "Information" in English.
input(data-i18n="[placeholder]common.enter_name") // Placeholder will be "Enter name here" in English.
button(data-i18n="common.send") // Button starts as "Send", but onSubmit, is changed to "Sending"
p Just have this in English # DNT
```

### View
```coffeescript
onSubmit: ->
  @$('button').text($.i18n.t('common.sending'))
```

## Resources
* [i18next](http://i18next.com/)