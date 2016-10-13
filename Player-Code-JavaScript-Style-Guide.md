We're teaching people [JavaScript](http://en.wikipedia.org/wiki/JavaScript). Therefore it is important that we have a consistent and clear coding style that is as close to standard JavaScript as possible. Every [Artisan](http://www.codecombat.com/contribute/artisan) should apply this coding standard in his levels to keep the code through all the levels consistent. This will lead to nice code, that can easily be read and prevents any form of confusion for players.

Just basically follow [the Node style guide](https://github.com/felixge/node-style-guide), but with these exceptions:

## Formatting
* The basic indention is **four** spaces. Tabs are not to be used at all.
* Try to keep lines to 60 characters or less. (We are working with very narrow code editors sometimes.)
* Use double quotes.

## Code style
* Always put `else` on its own line.
* Use `index++`, not `++index`.
* Don't use the ternary operator.

## Function and variable naming
* Avoid single letter names. Be descriptive with your naming.
* Event handler functions should be prefixed with the word `on`, like `onLoad`
* Try to declare local variables as near to their use as possible; try to initialize every variable.
```javascript
// Bad
function foo(x) {
    var a = 5;
    if(x < 5) {
        return x * x;
    }
    return x + a;
}

// Good
function foo(x) {
    if(x < 5) {
        return x * x;
    }
    var a = 5;
    return x + a;
}
```

## Booleans
* Do not compare `x == true` or `x == false`. Use `x` or `!x` instead.
* Compare objects to `null`, numbers to `0` or strings to `""` if there is chance for confusion.
* Use shortcuts.
```javascript
// bad
if (name !== '') {
    // ...stuff...
}

// good
if (name) {
    // ...stuff...
}

// bad
if (collection.length > 0) {
    // ...stuff...
}

// good
if (collection.length) {
    // ...stuff...
}
```

# Summary of [the Node style guide](https://github.com/felixge/node-style-guide) rules we're using

## Formatting
* No trailing whitespace.
* Use semicolons.
* Opening braces go on the same line.
* Declare one variable per var statement.

## Naming Conventions
* Use lowerCamelCase for variables, properties and function names.
* Use UpperCamelCase for class names.
* Use UPPERCASE for Constants.

## Variables
* Use trailing commas in Object/Array creation.
* Put short declarations on a single line.
* Only quote Object keys when necessary.

## Conditionals
* Use the === operator.
* Use descriptive conditions.

## Functions
* Write small functions.
* Return early from functions.
* Name your closures.
* No nested closures.

## Comments
* Use `//` for comments, not `/* */`.