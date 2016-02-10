## Problem
You want to reference the data stored inside a element's data attribute
## Solution
Use jQuery's built-in data accessing method `data('data_tag')`.
## Details
Given an element with a properly formatted data tag: `data-[data_tag]`.
```jade
- var helloWorld = "Hello, World!";
div#foo(data-bar=helloWorld)
```
Use jQuery's data function, we find the data assigned to `data-bar`.
```coffeescript
elem = $('#foo') # Returns a jQuery object.
importantString = elem.data('bar') # Pulls the data from the 'bar' data field.
console.log importantString # Output: Hello, World!
```
## Resources
* [jQuery](http://jquery.com/)
 * [data()](https://api.jquery.com/data/)
* [CoffeeScript] (http://coffeescript.org/)
* [Jade](http://jade-lang.com/)