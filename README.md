shields-tests
=============

Experimental test suite for [Shields][].

[Shields]: https://github.com/badges/shields


Features
--------

### Test vendor services

These tests use [Nock Back][].

By default, this test uses recorded http calls, allow additional http calls,
and doesn't record anything. It's useful for developing new tests.

    SHIELDS_DIR=/path/to/shields npm run test:vendor

There is [a bug it seems][bug], that prevents this from working correctly when
some fixtures are already recorded for the same hostname. To work around that,
delete `fixtures.json` and try again.

When you have written your tests, record the http calls:

    NOCK_BACK_MODE=record SHIELDS_DIR=/path/to/shields npm run test:vendor

Then you can run them in "lockdown" mode, which will use the recorded calls
and raise errors for any unexpected calls.

    NOCK_BACK_MODE=lockdown SHIELDS_DIR=/path/to/shields npm run test:vendor

> Pro tip: To run a single `it` or `describe`, change to `it.only` or
> `describe.only`.

[Nock Back]: https://github.com/node-nock/nock#nock-back
[bug]: https://github.com/node-nock/nock/issues/870


### Generate coverage reports

    SHIELDS_DIR=/path/to/shields npm run test:vendor:coverage
    opn coverage/lcov-report/index.html


### Test that the service endpoints in try.html return valid SVG

    SHIELDS_DIR=/path/to/shields npm run test:basic

Note: This test will hit all the external services.


### Developer convenience

Start a shields server on port 1111:

    SHIELDS_DIR/path/to/shields npm run start

> Pro tip: If you're developing regularly, set `SHIELDS_DIR` in your shell
> startup files.


License
-------

This project is in the public domain.
