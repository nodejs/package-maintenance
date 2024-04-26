# Proposal: Revise Downloads Page

As part of achieving the second [goal](./goals.md):

> Install Node.js and a package manager for a local development environment.

Our view is that the optimal way to install Node.js and bootstrap components like a package manager is through one or more external tools.

As an initial step towards this, we should revise the Node.js download page, https://nodejs.org/en/download, so that the primary download instructions suggest installation via one or more tools that provide for managing the versions of the Node.js runtime and of a package manager.

The current primary download method, a link to an installer, would still be an option available in one of the download page’s tabs; but it would no longer be the default method. This is because the installer link is only appropriate for certain target users, such as those who use Node.js for running scripts, and not for our primary target user group of application developers. Our default recommendation should be targeting our default set of users, and therefore it should recommend installing via one or more tools that make it easy to manage the runtime and package manager per project.

We should do this revision now, without predicating it on any changes to the Node.js distribution or on creating new tools. Once the page is rewritten, hopefully it should be apparent where any distribution changes or new tools might provide for an improved developer experience, and we can pursue ideas in those directions.
