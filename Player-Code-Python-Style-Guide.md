We're teaching people [Python](https://en.wikipedia.org/wiki/Python_(programming_language)). Therefore it is important that we have a consistent and clear coding style that is as close to standard Python as possible. Every [Artisan](http://www.codecombat.com/contribute/artisan) should apply this coding standard in her levels to keep the code through all the levels consistent.

Just basically follow [PEP 8](https://www.python.org/dev/peps/pep-0008/), but with these exceptions:

## Formatting
* Try to keep lines to 60 characters or less. (We are working with very narrow code editors sometimes.)
* Use double quotes.

## Code style
* Use camelCase, not snake_case, for compatibility with CodeCombat APIs.

## Function and variable naming
* Avoid single letter names. Be descriptive with your naming.
* Event handler functions should be prefixed with the word `on`, like `onPetSpawn`