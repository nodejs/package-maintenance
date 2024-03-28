## Package Maintenance Working Group Charter

The Node.js Package Maintenance Working Group is jointly governed by the members
of that Working Group (WG), and maintains oversight of its constituting teams:
the `@nodejs/package-maintenance` and `@nodejs/corepack` teams.

The WG responsibilities include:

* Management of the "version management tools" shipped with the Node.js distribution (see below).
* Management of repositories within the [pkgjs](https://github.com/pkgjs)
  GitHub organization including but not limited to:
    * Managing the list of organization owners which supplement the standard
      Node.js organization owners as outlined in:
[https://github.com/nodejs/admin/blob/master/GITHUB_ORG_MANAGEMENT_POLICY.md#owners](https://github.com/nodejs/admin/blob/master/GITHUB_ORG_MANAGEMENT_POLICY.md#owners)
    * Overseeing new repositories (creating, moving, removing).
    * Managing the maintainer teams for all of the repositories.
    * Contribution policy for repositories.
* Technical direction for the projects within
  the [pkgjs](https://github.com/pkgjs) organization.
* Project governance and process (including this policy).
* Managing the maintainer teams and contribution policies for the
  following repositories:
  * nodejs/ci-config-travis
  * nodejs/ci-config-github-actions
  * nodejs/package-maintenance

For the current list of WG members, see the project [README.md][].

[README.md]: ./README.md#current-project-team-members

### Version Management Tools

The WG has authority over Version Management solutions in the project including:

* Maintaining the relationship[^note] with any tools included in the Node.js default distribution with the express purpose of the following:
  - Download or install additional software from sources outside the default distribution.
  - Download or install additional Node.js distributions (default or third-party).
* Contribution policy for all of the additional software included in the Node.js distribution as qualified above.
* Conduct guidelines for the Version Management group.
* Recommend technical solutions for Version Management for the Node.js ecosystem.

[^note]A note on the meaning of "maintaining the relationship":

This means proposals to change the relationship between Node.js and npm or other tools (from either side) should be presented to the PMWG first to work out the details of the proposed changed.

## Collaborators

For the current list of WG members, see the project README.md.

This GitHub repository is maintained by the WG (all teams WG
members are Collaborators for the repository) and additional
Collaborators who are added by the WG on an ongoing basis.

Individuals making significant and valuable contributions are made
Collaborators and given commit-access to the ad-hoc repository.
These individuals are identified by the WG and their addition
as Collaborators is discussed during the WG meeting.

**Note**: If you make a significant contribution and are not considered for
commit access, log an issue or contact a WG member directly and it will
be brought up in the next WG meeting.

Modifications of the contents of this repository are made
on a collaborative basis. Anybody with a GitHub account may propose a
modification via pull request and it will be considered by the project
Collaborators. All pull requests must be reviewed and accepted by a
Collaborator with sufficient expertise who is able to take full responsibility
for the change. In the case of pull requests proposed by an existing
Collaborator, an additional Collaborator is required for sign-off. Consensus
should be sought if additional Collaborators participate and there is
disagreement around a particular modification. See Consensus Seeking
Process below for further detail on the consensus model used for governance.

Collaborators may opt to elevate significant or controversial modifications,
or modifications that have not found consensus to the WG for discussion by
assigning the WG-agenda tag to a pull request or issue. The WG should serve
as the final arbiter where required.

## WG Membership

WG seats are not time-limited. There is no fixed size of the WG.

There is no specific set of requirements or qualifications
for WG membership beyond these rules.

The WG may add additional members to the WG by consensus(defined
as no objections, more than 50% of the members participating in the
discussion, and all those participating in the discussion agreeing).

A WG member may be removed from the WG by voluntary resignation,
by unanimous consensus of all other WG members, or by a TSC decision. If a
member is removed from the WG then they are also removed from all WG teams.

Changes to WG membership should be posted in the agenda, and may be
suggested as any other agenda item (see "WG Meetings" below).

If an addition or removal is proposed during a meeting, and the full WG
is not in attendance to participate, then the addition or removal is
added to the agenda for the subsequent meeting, or taken async
that all members are given the opportunity to participate in all
membership decisions. If a WG member is unable to attend a meeting
where a planned membership decision is being made,
then their consent is assumed.

No more than 1/3 of the voting WG members may be affiliated with the same
employer. If removal or resignation of a WG member, or a change of
employment by a WG member, creates a situation where more than 1/3
of the WG membership shares an employer, then the situation must be
immediately remedied by the resignation or removal of one or more
WG members affiliated with the over-represented employer(s).

## WG Meetings

The WG meets regularly, check the foundation calendar for details.
One of the WG members will volunteer to act as the moderator
for each meeting subject to agreement from the rest of the
members. Each meeting should be published to YouTube.

Items are added to the WG agenda that are considered contentious or are
modifications of governance, contribution policy,
WG membership, or release process.

The intention of the agenda is not to approve or review all patches;
that should happen continuously on GitHub and be handled
by the larger group of Collaborators.

Any community member or contributor can ask that something be
added to the next meeting's agenda by logging a GitHub Issue.
Any Collaborator, WG member or the moderator can add the item
to the agenda by adding the WG-agenda tag to the issue.

Prior to each WG meeting the moderator will share the Agenda with
members of the WG. WG members can add any items they like to the
agenda at the beginning of each meeting.

The WG may invite persons or representatives from certain
projects to participate in a non-voting capacity.

The moderator is responsible for summarizing the discussion of
each agenda item and sends it as a pull request after the meeting.

## Consensus Seeking Process

The WG follows a Consensus Seeking decision-making model.

When an agenda item has appeared to reach a consensus the moderator
will ask "Does anyone object?" as a final call for dissent from the consensus.

If an agenda item cannot reach a consensus, any WG member can call for a
vote. Proposing a vote should follow the usual pull request approval process,
with the exception that WG members can object to a vote taking place. If
consensus cannot be reached on the wording of a vote proposal, each party can
suggest their own wording and they'll both be included in the vote proposals.
Vote should be counted using the Condorcet method, the winning proposition
is the one that beats all the other propositions.

Note that changes to WG membership do not follow the the process,
see "WG Membership" above.

## Onboarding

The process for adding new WG members is the following:

* A PR is open to add the new member to the list on the README.
* The nominee manifests their interest (in case of a self-nomination, this step can be skipped).
* The PR receives at least one approval and no objections.
* After 7 days, the PR can merge.

## Offboarding

* A PR is open to remove the individual from the list in the README.
* The PR merges if the condition for revoking WG membership are met
  (see "WG Membership" above).
* The individual is removed from all the teams in the oversight of the WG.
* The individual is removed from the nodejs GitHub org unless they are member
  for a reason other than WG membership.
  
