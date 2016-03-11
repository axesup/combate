## Problem

You want to add a route to the server

## Solution

Add an express route to [index.coffee](https://github.com/codecombat/codecombat/blob/master/server/routes/index.coffee). Construct it with [middleware](https://github.com/codecombat/codecombat/tree/master/server/middleware). Make sure to [test your endpoint](https://github.com/codecombat/codecombat/tree/master/spec/server/functional).

## Resources
* [Express Middleware](http://expressjs.com/en/guide/writing-middleware.html)
* [Jasmine](http://jasmine.github.io/2.4/introduction.html)
* [Node.js Flow (part 2) - Fibers and Generators](http://blog.vullum.io/nodejs-javascript-flow-fibers-generators/): Read this if you want a great explanation for what's going on when we use [generators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_Generators), [co-express](https://github.com/mciparelli/co-express) and [bluebird](http://bluebirdjs.com/docs/getting-started.html).