## Problem

You want to write tests for the client (in `app/`) code you're writing.

## Solution

Add a `spec` file to `test/app` which mirrors the location of the file being tested (`test/app/views/FooView.spec.coffee` for `app/views/FooView.coffee`). Use [jasmine](http://jasmine.github.io/2.4/introduction.html) and [jasmine-ajax](https://github.com/jasmine/jasmine-ajax) to write your tests and mock network requests. Your test can be run at [[http://localhost:3000/test]] when running the dev environment.

## Details

Since [TestView.coffee](https://github.com/codecombat/codecombat/blob/master/app/views/TestView.coffee) is simply another view in the site, it behaves like any other: it reloads whenever a file changes. Use this for fast code-test iteration!

We run a slightly altered version of jasmine-ajax, which includes functions `all` and `sendResponses`. See [vendor/scripts/jasmine-mock-ajax.js](https://github.com/codecombat/codecombat/blob/master/vendor/scripts/jasmine-mock-ajax.js).

## Resources
* [jasmine 2.4](http://jasmine.github.io/2.4/introduction.html)
* [jasmine-ajax](https://github.com/jasmine/jasmine-ajax)