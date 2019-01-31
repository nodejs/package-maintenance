## What?
Guidelines for CI/CD automation templates.

## Why?
Provide a baseline, common set of CI/CD infrastructure that can be relied upon regardless of what CI/CD providers are used by a project.

## How?
These guidelines are intended to be just that – guidelines. We will also include templates for common CI/CD providers and accept contributions of templates that implement these guidelines from the community.

It's worth noting that projects **do not** need to use one of the provided templates, but **do** need to ensure that their CI/CD setup enables them to follow the required guidelines at the very minimum. Projects are by no means restricted to the required guidelines – more complex and dynamic configurations are more than welcome.

## CI/CD Templates Should Include:

- Tests
  - Criteria (**Required**):
    - `npm test`
      - This can be any testing framework exposed via `npm test`.
      - Many CI/CD systems run this implicitly for JavaScript projects. You do not need to explicitly define `npm test` in these cases.
  - Criteria (**Optional**):
    - code coverage
      - failure if code coverage is below a well-documented threshold
- Caching
  - Criteria (**Required**):
    - At a minimum, cache `node_modules` (or equivalent) for your project
- Operating System Versions
  - Criteria (**Required**):
    - Windows
    - macOS
    - Linux
      - At least one current and one LTS release
      - Ubuntu is suggested but not required
- Node.js Versions
  - Criteria (**Required**):
    - nodejs@current
    - nodejs@lts
      - This includes all active and maintenance versions
  - Criteria (**Optional**):
    - nodejs@nightly
