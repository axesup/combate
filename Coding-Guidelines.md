Any given software project does well to follow certain common rules. It's not so much that any given rule is better than another, but rather consistency is valuable so that, if everyone knows and follows the rules, decision paralysis is avoided, the project is more organized and easier to work on as a group.

## Code Style

**There's still plenty of code in CodeCombat that doesn't follow these conventions. If you find any, please fix it.**

We follow the [CoffeeScript Style Guide](https://github.com/polarmobile/coffeescript-style-guide) and [CSS Style Guide](https://github.com/styleguide/css) with these additions:

* For the sake of brevity, names that need to incorporate "CodeCombat" can be abbreviated to "Coco" (for CS) or "coco" (for Sass).
* Names that have acronyms such as "id" or "html" should be capitalized the same as word for CamelCase names. So `getId()` instead of `getID()`, `ajaxToHtml` instead of `ajaxToHTML`. (Is `id` an acronym? ... Sure!)
* Lines should generally be no more than 119 characters, but for long comments or lengthy data, it's fine to exceed this amount. We recommend enabling soft-wraps on your editor.
* We don't use [spaces around default parameter values](https://github.com/polarmobile/coffeescript-style-guide#whitespace-in-expressions-and-statements): `containsPoint: (p, withRotation=true)` instead of `containsPoint: (p, withRotation = true)`. (We did a lot of Python in our youth.)
* We carelessly mix single and double quotes. Guess we could [fix this](https://github.com/polarmobile/coffeescript-style-guide#strings).
* We prefer [standalone `@` instead of `this`](https://github.com/polarmobile/coffeescript-style-guide#miscellaneous).

Note that Brunch automatically fails to compile when certain rules aren't followed, using a selection of [CoffeeLint](http://www.coffeelint.org/) rules. Keep an eye out for rule failures in Brunch output for guidance here.

## JavaScript Code Style

We use the tool [StandardJS](https://standardjs.com) to keep our JavaScript consistent.
This is an opinionated tool that helps us keep a consistent style and lint common problems.

The commands listed below can be slow and it's recommended to install an [editor plugin](https://standardjs.com/#are-there-text-editor-plugins) for faster feedback.

### Command Reference

`npm run fix` will run `standard --fix` on the entire codebase ignoring certain directories.

`npm run fix <filename>` will run `standard --fix` on a single file.

`npm run standard` will provide linting info for the entire project.

`npm run standard <filename>` will provide standard linting info for a single file.


## Commenting

Try to avoid writing low-value comments. Comments should be mainly used to flag areas in need of improvement or that really need some explaining. Ideally, code should be structured so that reading the raw logic reveals what it is doing and how it is doing it. If a function is long and convoluted, break it down into many clearly named functions. If it's not clear what a function does, rename or otherwise refactor it to make things clearer.

## Breaking CodeCombat Down Into Third-Party Modules

[Aether](https://github.com/codecombat/aether) and [Treema](https://github.com/codecombat/treema) are built from the ground up to be modular and not tied to CodeCombat, because they're large projects that we could imagine being used in a variety of other projects. There are other parts of CodeCombat which could be spun off into separate, fully autonomous projects. These projects do need to be fully autonomous, though, in terms of code. Treema and Aether are built not to have anything specific to CodeCombat. If more parts are to be spun off, they need to be generalized enough to be useful to others and without irrelevant cruft.

## Leveraging Third-Party Tools

CodeCombat uses a great many open source libraries for both [client](https://github.com/codecombat/codecombat/blob/master/bower.json) and [server](https://github.com/codecombat/codecombat/blob/master/package.json), and are summarized in the [wiki](https://github.com/codecombat/codecombat/wiki/Third-party-software-and-services). Familiarize yourself with these tools and use them whenever possible. Try to avoid re-inventing any of the many wheels included in the codebase. In particular, read through the documentation on [Backbone](http://backbonejs.org/), [Bootstrap](http://getbootstrap.com/), [Lodash](https://lodash.com/docs), and [jQuery](https://jquery.com/).