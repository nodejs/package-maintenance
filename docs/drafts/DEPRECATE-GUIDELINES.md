# What?

Guidelines for identifying and marking unmaintained packages.

# Why?

Provide a baseline and common practices for handling packages that are unmaintained.

# How?

These guidelines exist to help with the course of actions to take in the event that a package becomes unmaintained.

## What consititutes an unmaintained package?

- The author is no longer responding to questions, issues, PRs, or making any updates.
- The author may have explicitly indicated that they will stop all activities on the package.
- A different package that's more active and the author acknowledged as the replacement.
- Critical issues exist for the package and not being addressed
  - Known vulnerabilities identified by `npm audit` or other parties
  - Package is known to fail for LTS NodeJS

## Identifying unmaintained package?

- check last activity on github issues and PRs.

  - mark package as unmaintained candidate if no response from author to issues or PRs within one year

- file high priority issues in the package's repo

  - if npm audit identified vulnerabilities that are critical
  - if package is broken or fail to install for a LTS release of NodeJS

  - if author indicate they are no longer interested in maintaining, then add as unmaintained candidate
  - if no response within three months, then add as unmaintained candidate.

## `npm deprecate` command

- npm already has the "deprecate" command, we should utilize this.

  - It allows updating the message - verified as of 02/05/2019
  - It can be undone by setting an empty message. ie: `npm deprecate package@1.0.0 ""`

  - It can be used to mark a version as deprecate while the package may be very active still.

## Mark abandoned/unmaintained

- Use a special `npm deprecate` message such as `"abandoned and unmaintained"` to mark a package as abandoned.

  - no need to publish a new package to mark it abandoned.
  - but only owners can `npm deprecate` a package.
  - if author simply can't be reached and package is very outdated, then need to contact npm to get access to deprecate package.

* A cli to allow `npm deprecate` a range of versions on a package.
* or `npm deprecate` versions with published date older than a given time

## Identify replacement

- If a package is fully unmaintained, then a replacement should be identify and add to the deprecate message.
- If no replacement exist, then should identify the safe versions to use in deprecate message.

## Encourage Author to deprecate versions

- File issue in repo to encourage author to deprecate a version that:
  - Has known critical bugs and should be avoided
  - Known to fail for LTS NodeJS
  - Has known critical vulnerabilities

## What user can do to avoid deprecate versions

- allow consumer to specify a specific version to use for a package through an `override` field in their package.json

Package override RFC https://github.com/aeschright/rfcs/blob/ca127d7c5fb7ecde534172d771351c0b8f819e79/accepted/0009-package-overrides.md
