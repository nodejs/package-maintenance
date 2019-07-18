# Express answers to the survey

## What are the biggest problems your package need to face?

With a long project history and a strong focus on feature support, we have struggled to make new feature updates while also keeping up with all the other things (docs, support requests, security updates, etc).

## What are the most time-consuming tasks?

Support and issue triage take the most time.  As an important entry point for the whole node.js ecosystem we get a fair bit of simple issues, often not even Express specific issues.

## Which are the most difficult thing to implement in your package ecosystem? (ex: CI/CD, Versioned API Docs, etc...)

Automated release process.  As it stands there is one release manager (@dougwilson).  He handles it well, but because of long existing security concerns there has been no great way to expand the circle to others.  He has some ideas (maybe willing to expand on them here?) which would manages some of the security concerns as well as making it possible for others to release.

## What do you think that is missing in your package ecosystem? (ex: CITGM, etc..)

- CITGM for sure.  Would have helped greatly with a core change which caused a bug in `on-finished`.
- Issue templates across all the repos
- More contributors

## What are the tasks that don't let you focus in the business code?

In the risk of being repetitive, user support requests take the most non-coding time.

## How is designed you process to add new maintainers in your package?

https://github.com/expressjs/express/blob/master/Contributing.md

## What type of automation could help you?

Release process automation with a focus on security. Also, automation on triaging and pointing new contributors to the most important tasks to work on.

## What are the most frequent problems?

Slow progress on new features.

## What would you like to do to us?

Helping point new contributors to the right areas.

After a discussion with @mhdawson, we identified a few key things the @expressjs/express-tc can do to help:

1. Identify 3 important key objective where we need champions.  Examples: http2, promise support in middleware, documentation.
2. Identify 10 issues which are the highest priority for the project (should probably align with the 3 main goals)
3. Identify "good first issues" and/or issues where new users can start getting involved easily

This will help the WG give direction to all of the people who want to help.

## What problems are due to your dependencies?

False or overblown security reports have caused multiple incidents. We pin our external dependencies which has the negative repercussion of more work to keep updates rolling out.  We do this because it prevents accidental security incidents from a permissive version range.

## Are your dependencies need of help?

Express is made up of many modules, most of which are directly supported by the Express core team.  So yes they also need help with recruiting new contributors and issue triage help.

## Do you have to contribute to your dependencies? Do you establish a good communication channel?

- Almost the entire dependency tree is directly maintained by the same people, so yes.  This is probably uncommon, but it helps keep things secure and bug free.
- The external deps are all installed with strict versions locking, but when issues arise it has not been a problem to get deps updated (@dougwilson maybe you can give more input here?)
