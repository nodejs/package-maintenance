# Which versions of node should library authors test against?

_tl;dr: we'd like to encourage package authors to make sure their Continuous Integration (CI) setup includes all supported Node.js "long-term support" (LTS) versions, as well as the Current stable release._

At the start of 2019, npm released a [list of top 1000 most downloaded packages](https://docs.google.com/spreadsheets/d/1lZDNYsLntwD2q9XaTw-XLuG0VpHH6cOV-Uoa7Y1aTSM/edit#gid=1745448509). We scanned that list to find that a large number of these packages have not been updated in over a year, but even if they have - they still did not include the latest Node.js LTS version (10.x at the time) in their Continuous Integration (CI) setup.<sup>1</sup>

It is important to note, that CI providers, including Travis (the de facto standard<sup>2</sup> in JavaScript package ecosystem) **might not be using LTS** as the default. There is [work in progress to change this](https://github.com/travis-ci/travis-build/pull/1747), however it is a good time to double check your testing configuration - in October 2019 Node.js 12.x will become the active LTS version and 13.x will be released. At the end of December 2019 Node.js 8.x will reach end-of-life.

## Why

The [release schedule](https://nodejs.org/en/about/releases/) of Node.js is set up to have a new release with breaking changes every 6 months. According to [semver](https://semver.org), each such release increments the major version number. Even-numbered releases (10, 12, etc) receive "long-term support" (30 months) and because of that only LTS versions are recommended to be used in production applications.

While library authors are free to chose any support policy<sup>3</sup> they prefer, their libraries are likely to be used in one of up to 3 supported LTS versions. We recommend to include all of these versions in the CI test matrix. At the time of writing this would mean Node.js 8 and 10. By January 2020 this will become 10 and 12.

Odd-numbered (11, 13, etc) Node.js releases typically become unsupported after 6 months when a new even-numbered release is made available. While it is generally recommended that production applications do not use non-LTS Node.js versions, for library authors the recommendation is different - we'd like to encourage you to include the Current version (at the time of writing - 12, in January 2020 - 13) in the test matrix, as this can serve as an advance warning for both - library authors and Node.js maintainers<sup>4</sup>.

The above recommendation is for the minimal set of versions that should be supported - if it is an option at all, we'd like to encourage everyone to support older versions as well.

Additionally, while it is recommended to use the latest version of a major release line, you may want to support some specific versions, e.g. 8.10.0 is used by AWS Lambda, even though 8.16.1 is available. If that is one of your support targets you will be unable to use some of the newer features in 8.x and you should be checking for that in CI.

## How: setting up your `.travis.yml`

Travis uses [`nvm`](https://github.com/nvm-sh/nvm) to install node, so you can use any version or keyword it supports in your [`.travis.yml`](https://docs.travis-ci.com/user/languages/javascript-with-nodejs/#specifying-nodejs-versions). This means that your setup should look something like this:

```
language: node_js
node_js:
  - node   # Current stable, i.e. 12 in October, 2019
  - lts/*  # Most recent LTS version, i.e. 10 in October, 2019
  - 8      # Explictly include the maintenance LTS version
``` 

When you use the keywords (`node`, `lts/*`), you will automatically start testing in new versions as they come out. This does, however, mean that you will also automatically _stop_ testing in versions that may still need to be supported.

Alternatively, you can use [Renovate](https://docs.renovatebot.com/node/) to automatically open pull requests with new versions to your `.travis.yml` by adding `{ "travis": { "enabled": true } }` in your `renovate.json`.

When you're testing with a Current (or nightly) Node.js version before it becomes LTS you can also enable [`allow_failures`](https://docs.travis-ci.com/user/build-matrix/#rows-that-are-allowed-to-fail) for it.

## How: dropping support for older Node.js versions

Maintaining an Open Source Software library can become a burden and it is unfeasible to expect that all versions of Node.js should be supported by library authors indefinitely. Changing the minimum Node.js version requirement is considered a breaking change and according to semver rules requires a major version of your package to be incremented.

You should also keep the [`engines` field](https://docs.npmjs.com/files/package.json#engines) in your `package.json` up to date to indicate supported versions.

## Footnotes

1. Out of top 1000 packages using Travis for CI, 315 had neither a variation of 10.x nor `lts/*` in their setup; ~150 of those had commits since 10.x was first released, of which ~120 had commits since 10.x became active LTS.
2. Out of top 1000 packages, 877 were pointing to GitHub repos with a `.travis.yml` file at the root in September 2019.
3. The [Package Maintenance Working Group](https://github.com/nodejs/package-maintenance/) is working on a way to [define your support levels](https://github.com/nodejs/package-maintenance/blob/master/docs/drafts/PACKAGE-SUPPORT.md) - we welcome discussions and contributions.
4. The Node.js project also runs some smoke tests using The [Canary in the Goldmine tool](https://github.com/nodejs/citgm).
