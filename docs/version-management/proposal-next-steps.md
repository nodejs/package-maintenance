Proposal: Next steps

As part of achieving the second [goal](./goals.md):

> Install Node.js and a package manager for a local development environment.

And following up on the [proposal to revise the downloads page](./proposal-revise-downloads-page.md), we propose the following next steps:

1. We should revise the Node.js download page to split apart the operating system package managers (Homebrew and Chocolatey) onto their own tab separate from the Node.js version managers (nvm and fnm) and the version managers tab should remain the default. This will further nudge users toward our recommendation of installing Node.js in a version-managed way.

2. Also on the download page, we should add instructions for installing package managers which node has at any point historically supported (Yarn and `pnpm`), plus any others to be determined by a new policy (yet to be proposed) to add and remove recommended package managers. These instructions should follow whatever recommendation we receive from those projects' maintainers.

3. Corepack's documentation should be moved out of the Node.js API documentation and into its own website, or accessible as Markdown files in the Corepack repo. Corepack is a separate project from `node` and intermingling its documentation within `node`'s is confusing; we don't do that for `npm` even though we distribute `npm`.

4. Once all of the above is complete, we should start recommending alternative workflows in case Corepack is removed from the Node.js distribution. Users who wish to continue using Corepack will be recommended to do so via the instructions available on the Node.js download page or in Corepack's documentation.

