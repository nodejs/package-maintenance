# Governance

## Overview

As a project grows and contributions and activity start to increase, establishing a good operating rhythm and workflow can go a long way towards helping a project run smoothly.  Detailing the project's motivations and  vision, maintenance and development cycles, and decision making and rules of conduct are just a few activities that can all be used to help keep a project healthy and happy.

The aim of this document is to provide thoughts and recommendations to project maintainers for ways they can organize, document, and ultimately establish a Governance model that can be applied to their own project's needs.

## Vision
It is always helpful to include a section that clearly states the solution space / objectives of the project.  This helps introduce the overarching vision of the project and help contextualize all further decision making.  (technical or otherwise).  Articulating the "why" of the project helps ensure maintainers and contributors alike are aligned on the direction of the project as so is a good candidate to put first.

## Team Organization

### Owners / Maintainers
Highlighting the current owner(s) and maintainers of the project helps communicate who the stakeholders are in the project as it relates to issue triage, PR feedback, and general advocacy for the project.

It is common that certain members of this group may get special permissions for actions like merging PRs, editing issues, etc, so that should also be documented here.  

An owner will typically be the administrator of the repository.

### Contributors
In some cases, projects can opt to invite members to the repository but with limited permissions.  This may include write access to a repository to facilitate branch creation and submitting PRs, but _not_ write access to the _**master**_ branch (or other protected branches).  

This is helpful for maintainers because they wouldn't have to clone a fork to test out the work, and also is less friction for contributors, who wouldn't have to maintain a fork.

> _As with owners and maintainers, enumerating the privileges and permissions of this group would also be recommended._

## Project Organization
There can be different models for how the project is structured / distributed and how the team is organized. This may the case with projects that use a monorepo structure or have a plugin like architecture, and are often building on top of a "core" or "cli" base package (`peerDependency` model).  As projects expand horizontally and vertically, delegating maintainers to oversee sections of code or packages in your project can help with scaling communication and ownership, in particular in regards to issue triage and PR reviews.  In addition, this helps build up subject matter expertise.

If your project groups multiple related packages (e.g. _transforms_, _middleware_, _plugins_, etc), consider how to govern those projects as they fan outwards, in particular when it comes to managing breaking changes, new APIs, and how that all cascades downstream to the users of the core package.

> It may be appropriate at this level that your project maintainers start meeting regularly to discuss and involve themselves in overall project governance and decision making together.


## Technical Organization

### Code Quality 
If the project has a preferred style guide, coding conventions, or other general rules around code quality, documenting those can be a good courtesy to those first time contributors to your project.  This can help prepare  contributions for such "housekeeping" tasks like minding the projects linting and formatting rules, expectations around writing unit test, or necessity around writing / updating documentation.

### RFC Process
It's often good to segment off, or flag certain issues as `RFC` in particular to communicate important changes, potentially breaking, that are deserving of deeper conversation and analysis.  Standing for [_"Request for Comment"_](https://en.wikipedia.org/wiki/Request_for_Comments), it is a good way to initiate high level changes to the project that can be set aside and reviewed periodically by the maintainers, or can be used by the maintainers to communicate back outwards to the community.

The idea being that the more you can communicate earlier, the better.

## Moderation / Documentation
Documentation is a great way to help communicate to new and current contributors what can be expected from the project overall and how to contribute to it.  This can be a good opportunity to detail the architecture and patterns found in the project with links and references being made available. 

Some important documents that can help quickly communicate general information about your project are:
* _README_ - A great way to quickly explain the purpose of your package, how to use it, and other key concepts for anyone new to your project.
* _Code of Conduct_ - Helps establish and ensure respectful communication for the project and how others should be treated.
* _Contributing Guidelines_ - A great way to highlight what should be expected from contributors when submitting PRs.  Often times this can include providing unit tests for new or fixed code, following expected code quality / formatting guidelines, and how to report bugs.
* _Governance_ - A document similar to this one, outlining how code, issues, and responsibilities are managed within your project.
* _License_ - It is highly encouraged that all open source repositories have a meaningful license file.

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
- [RomeJS Governance](https://github.com/romejs/rome/blob/main/GOVERNANCE.md)
