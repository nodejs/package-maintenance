# Dependency management

## What

This document outlines the best practices on keeping package dependencies (incl. Node itself) up to date.

## Why

One of the basic maintenance tasks is ensuring that the package uses the latest stable versions of its dependencies. Here are some reasons why it's a good practice to do so:

- Having latest bugfixes / features
- Software release lifecycle
- Security

Potential caveats to take into consideration:

- Node.js version support
- Effects on the peer dependencies, incl. `node_modules` bloat

It is also important to make sure to test with latest LTS and current Node.js versions in CI/CD.

- [Choosing the Node.js version for testing](https://medium.com/@nodejs/choosing-the-node-js-versions-for-your-ci-tests-hint-use-lts-89b67f68d7ca)

## How

- Defining version ranges in `package.json`
- Using `npm outdated`
- Using `npm update`
- Using lockfiles
- Tools to automatically manage updates
    - Greenkeeper
    - Renovate
    - Dependabot
