# Testing

### Why?
Testing is awesome!

Testing is useful for developing new features, refactoring with confidence, and making sure new things don't break old things. When other people rely on your code for their own applications, testing helps you make sure things don't break for more than just yourself!

Testing is even more important when new maintainers take over a package. Sometimes when we work on a codebase for a long time we forget to articulate all the cognitive load to which we have become accustomed. Good test coverage can alleviate this burden.

### How?
It is a good idea to have unit tests, coverage that matches most use cases for the module, and make sure things work in all supported environments.

* **unit test**: test your code
* **integration test**: test your code with other applications dependencies
* **acceptance test**: test your application sticks in performance, heavy load, etc..

Here are some things to consider as you develop your package.

Some useful tools:
* [c8](https://www.npmjs.com/package/c8)
* [citgm](https://www.npmjs.com/package/citgm)
* [Codecov](https://www.npmjs.com/package/codecov)
* [Coveralls](https://www.npmjs.com/package/coveralls)
* [Jest](https://www.npmjs.com/package/jest)
* [Mocha](https://www.npmjs.com/package/mocha)
* [Nock](https://www.npmjs.com/package/nock)
* [nyc](https://www.npmjs.com/package/nyc)
* [tape](https://www.npmjs.com/package/tape)
