This is not an exhaustive list, but these are the most important for you to know about. We rely heavily on open source code and high quality services to speed development and focus on building CodeCombat, and these tools are what inspire us to open source our own work as well: to give back to the community that has given us all this. 

You don't need to learn how to use all of these tools, but please take some time to familiarize yourself with at least the ones you'll be using for the area(s) you'd like to work on.

## Core Languages

* [CoffeeScript](http://coffeescript.org/): Used throughout the site instead of JavaScript. If you're familiar with Python or Ruby then you'll feel right at home. If you're familiar with JavaScript, you'll find CoffeeScript seeks to fix many of JavaScript's faults and, we think, does a pretty good job.
* [Jade](http://jade-lang.com/): HTML needs to be rendered on the client. Jade files get compiled into JavaScript functions that, given a context object, returns an HTML string. All our pages are written in Jade; use it rather than other HTML generation methods like jQuery.
* [Sass](http://sass-lang.com/guide): These are compiled in to CSS files and provide many nice features CSS does not have.
* [Markdown](http://daringfireball.net/projects/markdown/basics): Used for static HTML strings, such as in database text documents or incorporated in some text-heavy Jade templates (see the legal page for an example). We use [Marked](https://github.com/chjj/marked) as our Markdown processor.

## Server-side

* [Node.js](http://nodejs.org/api/): The web server.
* [Express](http://expressjs.com): The web framework.
* [MongoDB](http://docs.mongodb.org/manual/): The database. Beyond standard collections, we also use the MongoDB search indexing and GridFS.

### Libraries available on the server
* [Passport](http://passportjs.org/guide/): Authentication. Right now we just use it for authentication through passwords, but one project is to expand the site's login options through it.
* [Mongoose](http://mongoosejs.com/docs/guide.html): An interface for MongoDB that turns documents into active records. We mainly use their plugin system to share certain logic between multiple collections, for versioning, naming, searching and permissions.
* [TV4](https://github.com/geraintluff/tv4): JSON-Schema validation. Whole other article on this subject.
* [Request](https://github.com/mikeal/request): Simpler request handling, used in testing to query the test server, and on the production server to interact with HTTP APIs for services like Facebook and Google.
* [Lo-Dash](http://lodash.com/docs) and [Underscore.String](https://github.com/epeli/underscore.string#readme): Great utility libraries.
* [Async](https://github.com/caolan/async): Various utility methods for doing all sorts of fun asynchronous tricks. We mainly have used its waterfall method to do a serial string of checks on User documents when they are changed.
* [Winston](https://github.com/flatiron/winston): Logging library for Node.js.
* [Bayesian Battle](https://github.com/codecombat/bayesian-battle): A library Michael wrote for ranking multiplayer skill based on one-on-one matches.

## Browser-side

### Site-wide Libraries

* [Backbone.js](http://backbonejs.org/): Provides a lot of the basic structure we use. The classes they provide are subclassed and extended. Each collection in the database has a parallel Backbone Model and each page on the site has one View which can contain many more Views. The Event system is also used, though perhaps underutilized for objects other than Views.
* [Validated-Backbone-Mediator](https://github.com/jamesflorentino/nanoScrollerJS): A mediator so wide-spread classes and views can communicate with one another more easily, now with JSON Schema validation.
* [jQuery](http://api.jquery.com/): Used largely for manipulating DOM elements. When it comes to utilities, Lo-Dash tends to be used instead.
* [jQueryUI](http://api.jqueryui.com/): autocomplete and others.
* [Keymaster](https://github.com/madrobby/keymaster): Keyboard bound events.
* [Bootstrap](http://getbootstrap.com/): Used mainly for styling and its JavaScript components. Scaffolding isn't really used.
* [Moment](http://momentjs.com/): Formats times and dates.
* [Treema](https://github.com/codecombat/treema): Custom built library for editing schema-defined JSON data. Used for all editors.
* [jsondiffpatch](https://github.com/benjamine/jsondiffpatch): Adds support for showing diffs and patching JS objects.
* [i18next](https://github.com/i18next/i18next): Handling our i18n needs (CodeCombat is translated into 45+ languages).
* [d3](https://github.com/mbostock/d3): Data vis!
* [Zatanna](https://github.com/differentmatt/zatanna): Manages CodeCombat-style autocomplete for the ACE editor.
* [nanoScroller.js](https://github.com/jamesflorentino/nanoScrollerJS): For when you need those scrollbars to get out of the way until you use them.
* [Modernizr](https://github.com/Modernizr/Modernizr): Helps with browser feature detection and fallbacks.
* [Flying Focus](https://github.com/NV/flying-focus): Makes it easier to see what your browser focus is doing.
* Lo-Dash, Underscore.String, and TV4 are also available in the browser.

### Gameplay Libraries and Services

* [CreateJS](http://www.createjs.com/#!/CreateJS): A suite of four libraries, all of which are used extensively for animation, tweening, sound and loading resources. It has its own internal event system, so that's used in lieu of Backbone events when required.
* [ACE](http://ace.c9.io/#nav=about): The code editor in game, and also used when editing code everywhere else on the site.
* [Box2D](http://box2d.org/): Physics engine.
* [Aether](https://github.com/codecombat/aether): Custom built library for running and deeply analyzing code. Used in gameplay to show things like what code is running at any given frame or where the code breaks and why. Transpiles multiple programming languages to JavaScript.
* [Firebase](https://www.firebase.com/): Service that synchronizes data between multiple clients. Used for synchronizing gameplay data when multiple people are playing on the same level. We also plan to use it for other inter-player communications, like chatting with friends or inviting other players to join in a campaign.
* [Firepad](http://www.firepad.io/): Collaborative text-editor built on top of Firebase, used in CodeCombat's code editor.

## Other tools
* [Jasmine](http://jasmine.github.io/2.0/introduction.html): Used for testing.
* [BrowserStack](http://browserstack.com): Used for browser compatibility testing.
* [Karma](https://github.com/karma-runner/karma): Test runner.
* [Brunch](https://github.com/brunch/brunch): Assembles the project, and is pretty much central to everything development.
* [Discourse](http://www.discourse.org/): Actually good forum software. CodeCombat is blessed by Jeff Atwood and Discourse.
* [SETT](http://sett.com): High-engagement blogging software. [Good for startup blogging.](http://blog.nickwinter.net/startup-blogging)