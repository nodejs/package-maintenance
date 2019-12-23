# Dependency management

## What

This document outlines the best practices on keeping package dependencies (incl. Node itself) up to date.

## Why

One of the basic maintenance tasks is ensuring that your package uses the latest stable versions of its dependencies. There are multiple benefits of doing this:

- The primary reason to keep your dependencies up to date is to receive all the latest bugfixes and improvements.
- Old versions of your dependencies might no longer be receiving security updates, which means that if a new serious vulnerability is disclosed, you may be forced to do extra unplanned work if you are multiple versions behind.
- Upgrading regularly in small incremental steps is potentially less disruptive than doing a big bang update to adapt to many breaking changes released over multiple versions of a dependency.

There are some potential caveats to take into consideration when upgrading dependencies:

- Dropping support for specific Node.js versions is normally considered a breaking change, which means that upgrading a dependency might imply that you also need to drop support for these versions, which in turn will force you to release a new major version of your package as well.
- In some cases, upgrading a dependency might result in incompatibilities with other packages which rely on peer dependencies, i.e. you may be increasing the size of the `node_modules` folder and/or static bundle.

Node.js itself can also be considered a dependency of your package, therefore you should make sure to test in latest LTS and current Node.js versions in your Continuous Integration system - see [Choosing the Node.js version for testing](https://medium.com/@nodejs/choosing-the-node-js-versions-for-your-ci-tests-hint-use-lts-89b67f68d7ca).

## How

- Choosing dependencies
- Defining version ranges in `package.json`
- Using `npm outdated`
- Using `npm update`
- Using lockfiles
- Tools to automatically manage updates
    - Greenkeeper
    - Renovate
    - Dependabot
