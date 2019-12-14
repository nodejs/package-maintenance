# Tools

The tools built by the package maintenance group to ease the adoption of the best practices defined
by this working group:

- [`package-compliant`](https://github.com/Eomm/package-compliant) validates the `support` section
of your `package.json`
- [Bevry's Automatic Maintenance Tooling](https://discuss.bevry.me/t/how-bevry-automates-maintenance-of-its-prolific-open-source-portfolio/693?u=balupton)
  - [`boundation`](https://github.com/bevry/boundation) asks you questions about your project, to automatically scaffold then maintain the project against the desired targets, including support for the following technologies
  - [`testen`](https://github.com/bevry/testen) tests your project against multiple node.js versions locally
  - [`editions`](https://editions.bevry.me) enables support for older node versions, as well as provides standardised data about the environments the package supports and what technology it uses
  - [`projectz`](https://github.com/bevry/projectz) enforces consistency of the meta files, such as the readme and package.json, and installation and license information, including badge information via https://github.com/bevry/badges
  - [dependabot](https://dependabot.com) configuration to auto-merge passing dependency updates
  - [`awesome-travis`](https://github.com/bevry/awesome-travis) has several scripts such as
    - [`awesome-travis/surge`](https://github.com/bevry/awesome-travis/blob/master/scripts/surge.bash) which publishes the commit, branch, and tag to surge for browsing of docs and cdn
    - [`awesome-travis/node-publish`](https://github.com/bevry/awesome-travis/blob/master/scripts/node-publish.bash) publishes git tags to `latest` and master (as configured by `NPM_BRANCH_TAG`) to the `next` tag
    - [`awesome-travis/node-install`](https://github.com/bevry/awesome-travis/blob/master/scripts/node-install.bash) ensures dev deps are installed with the desired node version, to enable tests to run even on legacy node versions
  - [`boundation-upgrade`](https://github.com/balupton/dotfiles/blob/master/.scripts/users/balupton/commands/boundation-upgrade) runs boundation on a project, and publishes a new release - if the engines changed, publishes a new major release, otherwise a minor
  - [`boundation-all`](https://github.com/balupton/dotfiles/blob/master/.scripts/users/balupton/commands/boundation-all) runs boundation-upgrade on all bevry's packages
  - [`valid-directory`](https://github.com/bevry/valid-directory) prevent publishing currupt file system structures to npm
