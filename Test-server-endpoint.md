## Problem

You want to write tests for a server endpoint

## Solution

Put tests which target the endpoint as a whole in /spec/server/functional. Use utility functions to clear models from the test db, create users, and so on. Use utils.wrap to perform asynchronous actions with yield and keep your tests flat.

## Details

### Test Data

Tests are run within the same process as the server, so tests can go in and use the same tools as the server and spy and mock as desired. It runs on top of a separate mongo, which is cleared at process start, so you'll need to create your own data for each test.

Note that the db **is not cleared** between each separate test during a run. Legacy tests depend on one another. Once all tests are refactored to be standalone, test will always start with a clear db by default. In the meantime, you'll need to clear relevant collections manually before each test.

### Globals

Globals are defined in [spec/server/common.coffee](https://github.com/codecombat/codecombat/blob/master/spec/server/common.coffee). The most important ones are listed here.

The global `getURL` function takes the path and turns it into an absolute url pointing to the test server.

```coffeescript
url = getURL('/db/article') # returns 'http://localhost:3001/db/article'
```

Most, if not all, models are global. Check common.coffee for a full list.

request is global. Be sure to use it, it has {jar:true} as a default option so that one request to the next maintains the same cookies. It also has been promisified by bluebird, so that it has functions such as `getAsync` and `postAsync` for your yielding needs.

### Co

[utils.wrap](https://github.com/codecombat/codecombat/blob/acba838db46b95cff67a7963f04ff76d84c190a9/spec/server/utils.coffee#L59-L62) is based on [co-express](https://github.com/mciparelli/co-express), a [succinct and elegant method](https://github.com/mciparelli/co-express/blob/master/index.js) which ties express and co together. `utils.wrap` ties co and jasmine together so that the function that is wrapped can throw errors and has `this` set to the jasmine test object. The vast majority of yield will either use request which has been promisified, or Mongoose whose functions already return promises.

```coffeescript
it 'is a jasmine test', utils.wrap (done) ->
  [res, body] = yield request.getAsync({uri: getURL('/db/article'), json: true})
  users = yield User.find({...})
  expect(...).toBe(...)
  done()
```

Don't forget to use `utils.wrap` and `yield` in your tests, or they won't run properly.

## Resources

* [Jasmine](http://jasmine.github.io/2.4/introduction.html)
* [Running Tests](https://github.com/codecombat/codecombat/wiki/Testing)