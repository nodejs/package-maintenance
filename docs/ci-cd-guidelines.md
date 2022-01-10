# Continuous Integration / Continuous Delivery (CI/CD)

## What

Guidelines for CI/CD automation templates to be shipped by the package-maintenance team.

> **Note:** This set of guidelines _is not_ about telling projects what they can and cannot do. Instead, it's a framework for those who are interested in building out bare-minium CI/CD templates for projects in the JavaScript ecosystem to use.

## Why

Provide a baseline, common set of CI/CD infrastructure that can be relied upon regardless of what CI/CD providers are used by a project.

## How

These guidelines are intended to be just that – guidelines. We will also include templates for common CI/CD providers and accept contributions of templates that implement these guidelines from the community.

It's worth noting that projects **do not** need to use one of the provided templates, but **do** need to ensure that their CI/CD setup enables them to follow the required guidelines at the very minimum. Projects are by no means restricted to the required guidelines – more complex and dynamic configurations are more than welcome.

## Definitions

Definitions for the various terms used in the guidelines:

### Required

To say a CI/CD template follows the "tests" guidelines documented here, it would need to meet all of the **required** marks. The same approach applies to for all other guidelines.

### Optional

**Optional** guidelines are, as the name indicates, optional for templates to include. They're _nice to have_ but by no means required.

## CI/CD Guidelines

- Tests
  - **Required**:
    - `npm test`
      - This can be any testing framework exposed via `npm test`.
      - Many CI/CD systems run this implicitly for JavaScript projects. You do not need to explicitly define `npm test` in these cases.
    - `npm ls`
      - If `npm ls` exits with a `0` exit code, your build should pass
      - If `npm ls` exits with a non-`0` exit code, your dependency graph is invalid and should fail the run
  - **Optional**:
    - code coverage
      - failure if code coverage is below a well-documented threshold
- Operating System Versions
  - **Required**:
    - Windows
    - macOS
    - Linux
      - All active LTS releases of Ubuntu or your CI provider's default Linux OS
- Node.js Versions
  - **Required**:
    - nodejs@current
    - nodejs@lts
      - This includes all active and maintenance versions
  - **Optional**:
    - nodejs@nightly
