## Run server tests

* Run `./bin/coco-mongodb` in one terminal
* Run `npm run jasmine` in another terminal

To run tests in just one file, run `npm run jasmine spec/server/path/to/some.spec.coffee`.

## Run client tests

* Start the [dev environment](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-General-Information#running-the-environment)
* Navigate to [[http://localhost:3000/test]]

## TravisCI

The CodeCombat GitHub account is hooked up to TravisCI, which runs all server and client side tests for each commit and pull request. You can see results of tests [here](https://travis-ci.org/codecombat/codecombat).

##

![](http://files.codecombat.com/BrowserStack%20logo.png)

We use [BrowserStack](https://browserstack.com) internally for test automation and our supported OS/Browser combinations.
