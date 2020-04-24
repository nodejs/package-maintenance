## Package Maintenance Working Group Governance

### Collaborators

### WG Membership

The package-maintence team has two levels of membership. Administrative
members and regular members. 

If you'd like to be listed as regular team member, open a PR adding yourself
to [MEMBERS.md](MEMBERS.md) along with a few words on how you are planning
to contribute to the team's efforts.

Administrative members take on additional levels of responsibility with
respect to managing the [pkgjs](https://github.com/pkgjs) organization
and the other repositories managed by the working group. Administrative
members should have a long standing involvement in the working group.

Individuals who have made significant contributions and who wish to be
considered as an Administrative member may create an issue or
contact an Administrative WG member directly. It is not necessary
to wait for an Administrative WG member to nominate the individual.

There is no specific set of requirements or qualifications for WG
membership beyond these rules.

The WG may add additional Administrative members to the WG by
consensus. If there are any objections to adding any individual
member, an attempt should be made to resolve those objections
following the WG's Consensus Seeking Process.

A WG member may be removed from the WG by voluntary resignation, or by
consensus of the Administrative WG members.

Changes to Administrative WG membership should be posted in
the agenda, and may be suggested as any other agenda
item (see "WG Meetings" below).

If an addition or removal is proposed, this should be raised in an 
issue, tagged for the next agenda, and concensus should be reached
in the issue. This is to ensure
that all Administrative  members are given the opportunity to
participate in all membership decisions. The addition or removal
is considered approved once the issue has been open for 2 meetings
or 14 days whichever is longer,and at least half the Administrative
members are in favor.

No more than 1/3 of the Administrative WG members may be
affiliated with the same employer. If removal or resignation
of a WG member, or a change of employment by a WG member,
creates a situation where more than 1/3 of the WG membership
shares an employer, then the situation must be immediately
remedied by the resignation or removal of one or more
Administrative WG members affiliated with the
over-represented employer(s).

For the current list of members, see the project [README.md][].

### WG Meetings

The WG meets regularly as scheduled on the Node.js
[calendar](https://nodejs.org/calendar). Each meeting should be
published to YouTube.

Items are added to the WG agenda that are considered contentious or
are modifications of governance, contribution policy, WG membership,
or release process.

The intention of the agenda is not to approve or review all patches;
that should happen continuously on GitHub. 

Any community member or contributor can ask that something be added to
the next meeting's agenda by logging a GitHub Issue. Any Collaborator,
WG member or the moderator can add the item to the agenda by adding
the ***package-maintenance-agenda*** tag to the issue.

Prior to each WG meeting the moderator will share the Agenda with
members of the WG. WG members can add any items they like to the
agenda at the beginning of each meeting. The moderator and the WG
cannot veto or remove items.

The moderator is responsible for summarizing the discussion of each
agenda item and sends it as a pull request after the meeting.

### Repository Management
All repositories under the management of the package maintenance team must include:

* LICENCE.md from the list approved by the OpenJS Foundation
* CODE_OF_CONDUCT.md referencing the Node.js Code of conduct in the admin repo.
* CONTRIBUTING.md which includes the current version of the DCO used by the Node.js Project
* An PR template(s) used for all Pull requests which includes the current version of the DCO used by the Node.js Project.
* A README.md which includes references to the GOVERNANCE.md in the package-maintenance repository as the authoritative governance which applies to the repository. 

#### nodejs/package-maintenance 

##### Maintainers

Maintainers for the nodejs/package-maintenance repo are managed
through the [package-maintenance](https://github.com/orgs/nodejs/teams/package-maintenance/)
team.  Administrative members are given the maintainer fole for that team
and can add/remove members as they join or leave the team.

##### Landing PRs

The package maintenance team policy on landing a PR in this repository
is for there to be:
- At least 4 approvals from rebular members
- No blocking reviews
- 7 day period from the 4th approval to merging

All PRs shall follow the [contributions policy](CONTRIBUTING.md)

#### nodejs/ci-config-travis

##### Maintainers

Maintainers for this repository are managed
through the [ci-condifg-travis-maintainers](https://github.com/orgs/nodejs/teams/ci-config-travis-maintainers/)
team. Administrative members are given the maintainer fole for that team
and can add/remove members as appropriate.

##### Landing PRs

The package maintenance team policy on landing a PR in this repository
is for there to be:
- At least 2 approvals from package-maintenance members 
- No blocking reviews
- 72 hours since the PR was openened 

#### nodejs/ci-config-github-actions

##### Maintainers

Maintainers for the repositories in the Pkgjs repository are managed
through the [ci-config-github-actions-maintainers](https://github.com/orgs/nodejs/teams/ci-config-github-actions-maintainers/)
team. Administrative members are given the maintainer role for that team
and can add/remove members as appropriate.

##### Landing PRs

The package maintenance team policy on landing a PR in this respositry
is for there to be:
- At least 2 approvals from package-maintenance members 
- No blocking reviews
- 72 hours since the PR was openened 

#### pkgjs organization

##### Adding or removing repositories

Any repository created under the Pkgjs.js GitHub Organization is considered to be
a project under the ownership of the OpenJS Foundation, and thereby subject
to the Intellectual Property and Governance policies of the Foundation.

Any member may request the management of repositories within the
Pkgjs GitHub Organization by opening an issue in the
[package-maintenance repository][nodejs/package-maintenance].
The actions requested could be:

- Creating a new repository
- Deleting an existing repository
- Archiving an existing repository
- Transferring a repository into or out of the organization

Provided there are no objections from any members raised in
the issue, such requests are approved automatically after 72 hours. If any
objection is made, the request may be moved to a vote
of the Administrative members.

In certain cases, OpenJS Cross Project Council and/or OpenJS Foundation Board
of Directors approval may also be required. (Most likely in the case of
transfeering a repository into or out of the organization).

##### Maintainers

Maintainers for the repositories in the Pkgjs repository are managed
through the [pkgjs-maintainers](https://github.com/orgs/nodejs/teams/pkgjs-maintainers/)
team.  Administrative members are given the maintainer role for that team
and can add/remove members as appropriate.

##### Landing PRs

The package maintenance team policy on landing a PR in the repositories within the Pkgjs
repository is for there to be:
- At least 2 approvals from package-maintenance members 
- No blocking reviews
- 72 hours since the PR was openened 

### Consensus Seeking Process

The WG follows a [Consensus Seeking][] decision-making model.

When an agenda item has appeared to reach a consensus the moderator
will ask "Does anyone object?" as a final call for dissent from the
consensus.

If an agenda item cannot reach a consensus a WG member can call for
either a closing vote or a vote to table the issue to the next
meeting. The call for a vote must be seconded by a majority of the WG
or else the discussion will continue. Simple majority wins.

Note that changes to administrative WG membership require
consensus. If there are any objections to adding or removing
individual members, an effort must be made to resolve
those objections. If consensus cannot be reached, a
vote may be called following the process above. Administrative
members are responsible for voting in these cases.

<a id="developers-certificate-of-origin"></a>
## Developer's Certificate of Origin 1.1

By making a contribution to this project, I certify that:

* (a) The contribution was created in whole or in part by me and I
  have the right to submit it under the open source license
  indicated in the file; or

* (b) The contribution is based upon previous work that, to the best
  of my knowledge, is covered under an appropriate open source
  license and I have the right under that license to submit that
  work with modifications, whether created in whole or in part
  by me, under the same open source license (unless I am
  permitted to submit under a different license), as indicated
  in the file; or

* (c) The contribution was provided directly to me by some other
  person who certified (a), (b) or (c) and I have not modified
  it.

* (d) I understand and agree that this project and the contribution
  are public and that a record of the contribution (including all
  personal information I submit with it, including my sign-off) is
  maintained indefinitely and may be redistributed consistent with
  this project or the open source license(s) involved.

[Consensus Seeking]: http://en.wikipedia.org/wiki/Consensus-seeking_decision-making
[nodejs/package-maintenance]: https://github.com/nodejs/package-maintenance
