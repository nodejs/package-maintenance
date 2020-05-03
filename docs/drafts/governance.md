# Governance

## Overview

As a project grows and contributions and activity increases, documentation on the project and the member(s) maintaining the project can help make managing expections amongst (new) contirbutors more manageable.  It can also present an oppourtunity to communicate the high level vision and goals of the project.

The aim of this document is to provide ideas and recommendations to project maintainers for ways they can organize and document their own project's governance to either help with things like code review delegation, ensuring consistent code quality standard, or what the project plan is.

## Vision
Starting with a section that clearly states the solution space / objectives of the project is a good way to introduce the overarching vision of the project and help contextualize all further decision making.  (technical or otherwise).  Articulating the "why" of the project helps ensure maintainers and contibutors alike are aligned on the direction of the project.

## Team Organization

### Owners / Maintainers
It is generally helpful to highlight the current owner(s) of the project, as well any maintainers.  This helps communicate who the stakeholders are in the project in regards to issue / PR feedback, and general advocacy for the project overall.

It is common that certain members of this group may get special permissions for actions like merging PRs, editing issues, etc, so that should also be documented here.

### Contributors
In some cases, projects can opt to invite members to the repository but with limited permissions.  This may include write access to a repository to create branches and submit PRs, but not write access to the _**master**_ branch (or other protected branches).  This is helpful for maintainers because they wouldn't have to clone a fork to test out the work, and also is less friction for conributors, who wouldn't have to maintain a fork.

> _As with owners and maintainers, enumarting the privileges and permissions of this group would also be recommended._


## Project Organization
Although not necessarily coupled, but how the project is structured / distributed and how the team is organized can be different models.  In particular projects that use a monorepo or have a plugin like architecture may have many related packages, often building on a "core" or "cli" base package.  As projects expand horizontally and vertically, delegating maintainers to oversee sections of code or packages in your project can help with scaling communication and ownership, as well as build up subject matter expertise.

If your project groups multiple related packages (e.g. _transforms_, _middleware_, _plugins_, etc), consider how to govern those projects as they fan outwards, in particular when it comes to managing breaking changes, new APIs, and how that all cacades downstream to the users of those packages.

> It may be apporopriate at this level that your project maintainers start meeting reguraly to discuss and involve themselves in overall project governance and decision making together.


## Technical Organization

### Code Quality 
If the project has a preferred styleguide, coding conventions, or other general rules for quality, documenting those can be a good courtesy to those looking to contribute to a new project.  This can help prepare new contributions for "housekeeping" tasks like minding the projects linting and formatting rules, expectations around writing unit test, or necessity around writing / updating documentation.

### RFC Process
It's often good to segment off, or flag certain issues as `RFC` in particular to communicate important changes, potentially breaking, that are deserving of deeper conversation and analysis.  Standing for [_"Request for Comment"_](https://en.wikipedia.org/wiki/Request_for_Comments) it is a good way to initiate high level changes to the project that can be set aside and reviewed periodically by the maintainers, or can be used by the maintainers to communicate back outwards to the community.

The idea being that the more you can communicate earlier, the better.

## Supplmental Documentation
Documentation is a great way to help communicate to new and current contributors what can be expected from the project overall and how to contribute to it.  

Some important documents that can help quickly communicate general information about your project are:
* _README_ - A great way to quickly explain the purpose of your package, how to use it, and other key concepts for anyone new to your project.
* _Code of Conduct_ - Helps establish and ensure respectful communication for the project and how others should be treated.
* _Contributing Guidelines_ - A great way to highlight what should be expected from contributors when submitting PRs.  Often times this can include providing unit tests for new or fixed code, following expected code quality / formatting guidelines, and how to report bugs.
* _Governance_ - A document similar to this one, outlining how code, issues, and responsibilities are managed within your project.
* _License_ - It is highly encouraged that all open source repos have a meaningful license file.

## GitHub
If you're using GitHub, here are some good features you can take advantage of to help automate and organize your project:
- [Projects and Milestones](https://github.com/features/project-management/)
- [Issue / PR Templates](https://github.blog/2016-02-17-issue-and-pull-request-templates/)
- [Code Owners](https://github.blog/2017-07-06-introducing-code-owners/)
- [Continuous Integration (GitHub Actions)](https://github.blog/2019-08-08-github-actions-now-supports-ci-cd/)
- [Discussions (beta)](https://github.com/dear-github/dear-github/issues/44)
- [Contributing Guidelines](https://github.blog/2012-09-17-contributing-guidelines/)

## Links / References
* NodeJS Governance, [[1](https://github.com/nodejs/node/blob/master/GOVERNANCE.md), [2](https://github.com/nodejs/node/blob/master/GOVERNANCE.md)]
* [UnifiedJS Governance](https://github.com/unifiedjs/collective#readme)
* [Rust RFCs](https://github.com/rust-lang/rfcs)
* [React Team](https://reactjs.org/community/team.html)
>>>>>>> first draft
