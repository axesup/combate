## Problem

You want the server to provide standard REST endpoints to the site.

## Solution

Create routes in `/server/routes/index.coffee`, using pre-existing or custom middleware in `/server/middleware`.

## Details

The routes we usually include for a collection are:

* Create: `POST /db/collection_name`
* Get many: `GET /db/collection_name`
* Get one: `GET /db/collection_name/:id`
* Edit one: `PUT /db/collection_name/:id`

Some collections may also allow DELETE, though that's uncommon. Others may not need all of these, such as one which allows creation but not editing.

### General vs Custom Behavior

There are generic handlers for standard behavior in [`/server/middleware/rest.coffee`](https://github.com/codecombat/codecombat/blob/master/server/middleware/rest.coffee), and if possible, your endpoints should just use those. If your endpoint needs custom behavior, though, you can use `rest.coffee` as a template for specific middleware, such as for the [PUT Achievement middleware](https://github.com/codecombat/codecombat/blob/8f16f5f487bfdab51f9490002a150fd15c3cbfb8/server/middleware/achievements.coffee#L14-L25).

You can also extend route behavior by chaining middleware, such as [these Achievement POST and GET routes](https://github.com/codecombat/codecombat/blob/8f16f5f487bfdab51f9490002a150fd15c3cbfb8/server/routes/index.coffee#L18-L19) do. The GET middleware `fetchByRelated` checks if there's a `related` is a GET query parameter. If there is, it handles the response, otherwise it continues to the generic rest GET middleware.

```
app.get('/db/achievement', mw.achievements.fetchByRelated, mw.rest.get(Achievement))
```

While the POST middleware prevents anyone but admins or artisans from performing the action.

```
app.post('/db/achievement', mw.auth.checkHasPermission(['admin', 'artisan']), mw.rest.post(Achievement))
```

### Generators and Yield

To avoid callback hell, we use `co`, which is elegantly tied to `express` with `co-express`. Async functions should return Promises, and then yielded to co. Mongoose commands like `find` and `save` return Promise-like Query objects. If you need to make a Node-style callback function into a Promise, use [Bluebird](http://bluebirdjs.com/docs/getting-started.html). When errors happen, they are automatically given to Express' `next` function and sent to our error middleware.

For an elegant explanation of what's going on when you use `co` and `yield`, read [Node.js Flow (part 2) - Fibers and Generators](http://blog.vullum.io/nodejs-javascript-flow-fibers-generators/) by Eirik Vullum.

```coffeescript
wrap = require 'co-express'

# this function is express middleware that can be put into any routes
module.exports.setSomeValue: wrap (req, res) ->
  doodad = yield Doodad.findById(req.query.userID)
  doodad.set('property', 'value')
  yield doodad.save()
  res.status(200).send(doodad.toObject())
```

## Resources
* [Mongoose with ES6](http://mongoosejs.com/docs/unstable/docs/harmony.html)
* [Bluebird](http://bluebirdjs.com/docs/getting-started.html)
* [co](https://github.com/tj/co)
* [Node.js Flow (part 2) - Fibers and Generators](http://blog.vullum.io/nodejs-javascript-flow-fibers-generators/)