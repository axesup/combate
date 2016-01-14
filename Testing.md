## Running server tests

* Run `./bin/coco-mongodb` in one terminal
* Run `npm run jasmine` in another terminal anytime you want to run tests.

To run tests in just one file, run `npm run jasmine spec/server/path/to/some.spec.coffee`.

## Running client tests in the terminal

* Run `./bin/coco-mongodb`
* Run `npm run brunch watch`
* Run `./bin/coco-client-test-runner`

A Chrome browser should appear. You can minimize it; it's karma running the tests. Whenever client side code changes or tests change, karma should run the tests from /test/app in that extra browser window and show results in the terminal.

## Client Side Code Coverage

Karma will generate reports using Istanbul when you run it. These files are in the 'coverage' folder in the root directory. Istanbul does not currently support codemaps, so we only really have a general sense of how much of the whole client has been covered, not which specific parts.

## Running client tests in the browser

Another way to run client tests, which is a bit easier to do, more flexible, and takes advantage of brunch's auto-reload ability, is to run the development environment as normal (coco-dev-server) and go to [http://localhost:3000/test/](http://localhost:3000/test/). This will run all client side tests in Jasmine's HTML test runner, and provide navigation for choosing specific test folders and files to run on the right. You can also click specific suites or tests to have them run individually.

Since this is running as a view within the browser, tests may run a little differently in this environment than when run with karma. You should check that the tests still run in karma.

## TravisCI

The CodeCombat GitHub account is hooked up to TravisCI, which runs all server and client side tests for each commit and pull request. You can see results of tests [here](https://travis-ci.org/codecombat/codecombat).