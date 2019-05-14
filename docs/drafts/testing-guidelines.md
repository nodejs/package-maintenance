# Testing

### Why?
Testing is awesome!

Testing is useful for developing new features, refactoring with confidence, and making sure new things don't break old things. When other people rely on your code for their own applications, testing helps you make sure things don't break for more than just yourself!

Testing is even more important when new maintainers take over a package. Sometimes when we work on a codebase for a long time we forget to articulate all the cognitive load to which we have become accustomed. Good test coverage can alleviate this burden.

### Updates
Node.js has a [strict release pipeline](https://nodejs.org/en/about/releases/) focused on continuous improvement and update. In order to guarantee to your users that the module you made works correctly with the newer version of Node.js, it is a good practice to run your tests across multiple Node.js versions.

This can be done developing a CI pipeline. Check out our [CI guidelines](https://github.com/nodejs/package-maintenance/blob/master/README.md).

The minimal versions you should focus are:
* LTS (long time support)
* Current

Of course, you are freely to maintain a package that run also with older versions of Node.js that reach the "end-of-life" stage.

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
