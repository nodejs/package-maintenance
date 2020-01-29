# Dependency management

## What

This document outlines the best practices on keeping package dependencies (including Node itself) up to date.

## Why

One of the basic maintenance tasks is ensuring that your package uses the latest stable versions of its dependencies. There are multiple benefits of doing this:

- The primary reason to keep your dependencies up to date is to receive all the latest bugfixes and improvements.
- Old versions of your dependencies might no longer be receiving security updates, which means that if a new serious vulnerability is disclosed, you may be forced to do extra unplanned work if you are multiple versions behind.
- Upgrading regularly in small incremental steps is potentially less disruptive than doing a big bang update to adapt to many breaking changes released over multiple versions of a dependency.

There are some potential caveats to take into consideration when upgrading dependencies:

- Dropping support for specific Node.js versions is normally considered a breaking change, which means that upgrading a dependency might imply that you also need to drop support for these versions, which in turn will force you to release a new major version of your package as well.
- Upgrading a dependency could result in increased size of the end user's `node_modules` / compiled bundle, if other packages in the ecosystem do not upgrade around the same time.

Node.js itself can also be considered a dependency of your package, therefore you should make sure to test in latest LTS and current Node.js versions in your Continuous Integration (CI) system - see [Choosing the Node.js version for testing](https://medium.com/@nodejs/choosing-the-node-js-versions-for-your-ci-tests-hint-use-lts-89b67f68d7ca).

## How

### Choosing dependencies

There is no single recipe for choosing the right dependency for your package, but there are some indicators to pay attention to and questions to ask yourself:

- Do you need a dependency at all? Each dependency has a download cost, and if it is build by someone else - it may have security and reliability implications.
- Does the package have tests and do they run automatically in a CI system, e.g. Travis or GitHub Actions.
- Is the package actively maintained? Lack of activity in the source control does not mean it is unmaintained, as it may simply be done, but it is something to pay attention to.
- Make sure the package is not already marked as deprecated on npm and in the README - authors may give you suggestions for alternatives.

### Defining the dependency version ranges

JavaScript ecosystem relies on [semantic versioning](https://semver.org/) and most packages respect its rules. Therefore, it is usually recommended that your `package.json` accepts new minor/patch releases of your dependencies automatically. This is the default behavior of npm - when you first `npm install [new dependency]`, it will by default prefix the version with a `^` to indicate that all new releases under the same major version are acceptable.

You may also use a tilde (`~`) character instead of the caret (`^`), to only accept bugfix (patch) releases, but this may mean that your dependency will become out of date sooner.

Accepting _all_ releases (i.e. `*` or `latest` instead of a version range, or an unbounded version range using `>`/`>=`) is risky and almost certainly will break your package unexpectedly when a new major version of the dependency is released.

Further reading:

- npm documentation: [About semantic version](https://docs.npmjs.com/about-semantic-versioning)
- npm documentation: [Updating packages downloaded from the registry](https://docs.npmjs.com/updating-packages-downloaded-from-the-registry)

### Using lock files

The lock files are a snapshot of your full dependency tree, incl. all sub-dependencies, their precise versions and also integrity hashes. Having a lock file allows npm to recreate the dependency tree exactly as it was. npm supports two lock files: `package-lock.json` and `npm-shrinkwrap.json`. Yarn uses its own lock file format.

The `package-lock.json` will get created automatically by default and it will not be published into the registry, i.e. it is only intended to be used for development purposes. npm recommends you commit this file into your source control.

You can chose to use the `npm shrinkwrap` command to instead create an `npm-shrinkwrap.json` file. It is the same in structure as the `package-lock.json`, but it will also be published together with your package in the registry, which means that not only people who develop the package, but also the users will receive the exact set of dependencies.

Using the lock files has downsides:

- `package-lock.json` (and `yarn.lock`) is only used in development, so you may be testing your package with a different set of dependency versions than your users will be using it, which may occasionally lead to unexpected results.
- no dependency updates will be received automatically with `npm install`.

You can disable the lock files in your global or local `.npmrc` file by adding a `package-lock=false` line. This does however mean that npm will also ignore the shrinkwraps included in your dependencies.

Further reading:

- npm documentation: [npm-package-locks](https://docs.npmjs.com/files/package-locks)

### Updating the dependencies manually

You can list outdated dependencies using the `npm outdated` command. If there are any in-range updates - you can use `npm update` command to install them.

You will need to modify your `package.json` version specifier to receive out-of-range updates.

There are several tools that will help you manage this from your local command line, such as [`npm-check`](https://www.npmjs.com/package/npm-check) and [`npm-check-updates`](https://www.npmjs.com/package/npm-check-updates), however you can also set up external tools to automatically create Pull Requests with updates. 

### Automatically keeping dependencies up to date

If your package has [automated tests](testing-guidelines.md) and [CI/CD](ci-cd-guidelines.md), you can use one of several services, free for Open Source Software, to automatically keep your dependencies up to date.

All of the below tools provide a GitHub App to create PRs with updates. They also support maintaining lock files to update sub-dependencies. Each tool also has built-in or community supported ways of automatically merging the PRs as long as tests pass, although this does carry some risk.

- [Dependabot](https://dependabot.com/)
    - Supports other languages, besides JavaScript 
- [Greenkeeper](https://greenkeeper.io/)
    - Creates branches to test even the in-range updates and reports status if they make tests fail
- [Renovate](https://renovate.whitesourcesoftware.com/)
    - Supports other languages, besides JavaScript
    - Supports updating `.travis.yml`, Circle CI yml and `.nvmrc`, i.e. it can update the Node.js version you use for running tests
- [Snyk](https://snyk.io/)
    - Supports other languages, besides JavaScript
    - Supports ignoring specific deps, and limiting the amount of open simultaneous PRs to reduce noise level
