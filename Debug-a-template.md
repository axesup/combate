## Problem

You want to see what's going on within a template while it is executing.

## Solution

Drop in `console.log` calls as you would inside a view.

## Details

Jade is compiled into a JavaScript function which takes a context object and returns an HTML string. You can use any JavaScript you'd like be prefixing with `-`.

```jade
for item in view.items.models
  - console.log('Looping through item', item);
  p= item.get('name')
```

## References

* [Code in Jade](http://jade-lang.com/reference/code/)