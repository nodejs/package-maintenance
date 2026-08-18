# Manage all the things you need to build with Node.js

## The History

Version Management is something the Node.js project has discussed a few times. Starting in *< INSERT HISTORY OF WG HERE >*. And more recently with the introduction of `corepack` for managing versions of package managers. While there has been a volume of discussions and code examples I do not believe there has been a cohesive technical document to bring it all together. This is my attempt at such a doc.

Node.js and the toolchain it ships with is used throughout the SDLC (software development lifecycle) and has different needs at different stages of work. For example, it is highly
uncommon for someone to use a different versions of anything within the same production deployment while is is highly common to do so for local development or CI.

This has led to a the Node.js project focusing on the well understood (but also highly complicated) aspect of simply supporting one locked version of the toolchain across the many
supported architectures. This is in fact a required area of investment for the project as no matter the local dev toolchain a team or developer chooses, when in prod it is *always*
necessary to support a secure and stable single version workflow.

This focus has left it to the ecosystem to solve for the local and CI workflows where many versions are commonly needed for a variety of tools. And when the ecosystem is in charge
a wonderful variety of solutions emerge. 

## The Problem

A realistic and productive Node.js development environment cannot be setup with *only* tools shipped within the current executables. A version manager for both the `node`
executable and a package manager is required.

## The Stakeholders

This proposal requires members of the community to work together. To help enable that, I propose we formalize the Package Maintenance Working Group (PMWG) to own this domain and be a
shared space for Node.js contributors, tooling authors, and interested community members to work. That would help ensure that all stakeholders in the ecosystem had a well
documented and clear idea of who to work with and how that process proceeds.

Once we have chartered the PMWG to take ownership of this domain we can expand on this proposal and other related document and policies around how the Node.js Project intends to
move forward with regards to Package Mangers, version managers, and associated tooling which are vendored or included in some from with the Node.js distribution.

## Use Case Scope

We cannot build all things for all people. To help keep focus within this proposal we want to focus on solving for one specific use case:

**Users installing Node.js on their local development machine or in CICD process for the purpose of building.**

This means we are not intending for this tool to be used to install on production servers. That is not only an already well covered use case, it is also not a place where
dynamically installing many runtime or tool versions is a good or recommended practice.

## Goals

1. A new solution should attempt to reduce redundancy in both concepts and metadata in package.json were possible
2. Reduce developer toil (as @GeoffreyBooth said: The most important part of this is that it defines the end goals: no lockfile mismatches, no failed builds.)

## Prior Art

There is alot here, adding a place holder to remember but not get distracted.

@TODO list out more about the current version managers and their approaches.

## A Proposal

Node.js ships or endorses (either builds or adopts an existing project) a version manager with the following qualities:

1. Manage versions of both `node` and a **small** subset of ecosystem tooling for local and CI environments
2. The tool should enhance the user experience for all supported tools in an equitable way (note on this below)
3. There is a clear and concise process for tools to be included (but as we are not trying to achieve equality, some tools are grandfathered in)
4. The technical solution (and all others considered) are well documented and clear to stakeholders
5. The technical solution should be reasonably approachable for our consumers without a lot of new education required

As there is already a lot of prior art in the ecosystem. I will venture to make a clear proposal for an end user experience we hope to achieve without picking an existing tool or
set of implementation details (hence the name `nver` as a placeholder):

```
$ curl -o- https://nodejs.org/dist/install.sh | bash
$ node --version # the latest lts version
$ npm --version # the npm version shipped with node
$ mkdir project && cd project
$ npm init -y
$ nver install npm@latest node@20.x
$ node --version # the local node version 20.x
$ npm --version # the local npm version newer than what was shipped with node at 20.x
```

While this is the "bootstrap from scratch UX" there are many other important workflows which led to the development of `corepack` which we should also well support. One such is
cloning down an existing project and ensuring that you have a properly setup development environment for working with it. Here is an example for that UX:

```
$ git clone git@github.com:nodejs/project.git && cd project
$ npm install
This project requires packages to be installed with pnpm@8.15.4 and node@^20.0.0.
We can help you set that up by answering yes to the prompt below, or after selecting
no you can run:

$ nver install

Continue? (yes)
...
$ pnpm install
```

You may notice in the above that the `npm` executable noticed that the project was not meant for use with `npm` and displayed a message to users. This proposal would include some
collaboration by our esteemed colleagues at the various supported packages managers to implement a common stub which would be maintained by the Node.js project which implements a
standard check. The inclusion of this stub would be a requirement for being included in the tooling. To achieve this we have been discussing a proposal in the Package Metadata Interop Collab
Space to add a `devEngines` field. More on that below.

And lastly, most developers work on more than one project at a time. It is important for their productivity that it is easy to switch between projects and their associated tooling.
Here is an example of working on multiple projects at once:

```
$ cd project1
$ npm it # install and test (assuming project is already configured or using defaults)
$ node --version
v20.11.1
$ cd ../project2
$ npm it
This project requires packages to be installed with yarn@1.22.21 and node@^18.0.0.
We can help you set that up by answering yes to the prompt below, or after selecting
no you can run:

$ nver install

Continue? (yes)
...
$ yarn install && yarn test
$ node --version
v18.19.1
$ cd ../project1
$ npm test # seamless switch back to node version
```

### Declaring development engines

Currently the only widely used way to declare development tooling is the `packageManager` field. This only covers one aspect of the problem (the package manager) and is not
designed in a way to allow for a more holistic approach more similar to the pre-existing `engines` field. In reality many projects have more broad requirements for development
tooling which they document in their project readme files or docs. Additionally, all projects which have native dependencies require an implicit version of `python` based on their
`node-gyp` version. These things are not covered under the current implementation of `packageManager` and they typically do not cause as much user issues when discrepancies arise
because they are less common and not "the first thing people run" but they are equally important to get correct.

To this point, I propose we work toward a slimmed down version of the proposed `devEngines` field which covers explicitly declaring these required development tools.  I say slimmed
down simply to differentiate it from the [version currently documented in the issue](https://github.com/openjs-foundation/package-metadata-interoperability-collab-space/issues/15)
(as of April 1 2024). The reason I propose slimming it down is to prevent the initial specification from defining ways tools should fetch these dependencies (aka dropping the
download section). Here is what I think we should adopt for a first pass:

```javascript
// package.json
{
  "devEngines": {
    // os: '', as specified in original proposal
    // cpu: '', as specified in original proposal
    // runtime: '', as specified in original proposal
    packageManager: {
      name: 'npm', // names which we would specify and map to individual known projects
      version: '', // this would be semantically left open from the spec, but should be considered the equivalent of npm package specifiers
      // see: https://github.com/zkat/ssri/blob/latest/README.md#--ssriparsesri-opts%E2%80%94integrity 
      resolved: {
        version: '1.0.0',
        uri: 'https://registry.url/path/to/tarball.tgz',
        // this would be the output of ssri
        digest: '...'
      }
    }
  }
}
```

With this slimmed down version, we can test out approaches with different tooling implementations for how we resolve, fetch, and install the dependency without forcing the hand of
tool authors into one single direction. If they wanted to limit that `version` cannot be a git repository, that would be acceptable even though `npm` defines that as valid for a
package specifier.

## Technical Approachs

There are three primary approaches which version managers can (and have, see examples) take to solving this problem:

1. `PATH` manipulation
2. In-process indirection
3. Jumper Binaries

We will describe each in the section below and attempt to well document the pros and cons of each approach.

### `PATH` manipulation

This approach is the most commonly currently deployed approach to binary version management. It is how `nvm` and other popular tools work.

**Pros:**

- Separation of concerns: keeps the version detection and indirection out of the main executable code

**Cons:**

- Support for the wide range of OSs and shells is a challenge

### In-process indirection

This approach uses a stub at the start of the program to load in the concrete implementation of the executable. [This approach is the current `corepack`
design](https://github.com/nodejs/corepack/commit/5ff6e82028e58448ba5ba986854b61ecdc69885b) and also has prior art in `coffeescript` (see example).

**Pros:**

- Separation of concerns: keeps the version detection and indirection out of the main executable code

**Cons:**

- It is slower than path manipulation on the most common path but still faster than jumper binaries
- Being in the main executable means even in situations where there is no need (production) the code is still run

**Links**

- [Coffeescript version loader](https://github.com/nodejs/node/issues/50963#issuecomment-1902202491)

### Jumper Binaries

Jumper binaries are specially crafted executable entry points which find the correct binary to run as a child process. This was the original `corepack` design.

**Pros:**

- Separation of concerns: keeps the version detection and indirection out of the main executable

**Cons:**

- It is slow (comparatively)
- Breaks tooling and user expectations of where to find the binary/source being run

### Considerations Needing to be Addressed

1. Node Binary install locations
1. Bootstrap phase cannot require node, needs to be cross platform
1. How do package managers do global installs? How do they perform `npm link` across node versions, etc.
1. Similar to the above, how does it handle installing npm/package managers across node verisons.
1. Opinions on installing versions. We should not have any hard ones (aka install any node version they ask for, even insecure ones with a flag)



---

# NOTES:

**equal vs equitable**: Equality means each individual or group of people is given the same resources or opportunities. Equity recognizes that each person has different circumstances and allocates the exact resources and opportunities needed to reach an equal outcome.


**@darcy**: I need to fit this all in here and I am not sure how and it was easier to start just copying it wholesale to start.

> Notably, I have not been in favor of: "jumper" binaries, net-new fields (like packageManager OR even devEngines - although I'm still participating with those discussions) or even the idea of a new path manip tool to manage node (as npx already does this). All of these are misguided imo (ie. why I have historically & continue to pushback on distributing corepack & don't think a new "node version manager" which uses similar concepts would be any better).
> Things everyone should understand &/or align on:
> There is value codifying your project's package manager & node version (this is widely agreed on)
> 1. Developers have put that information in engines historically (this is debated by a vocal minority & I do not agree with them - here's 1.3M examples)
> 2. Package managers have supported checking the package manager version & node version from engines since it was first introduced by npm more then a decade ago (this is a fact)
> 3. If we all agreed on the above then we would likely avoid the pursuit of adding new fields. I have & continued to debate these points with individuals even though they are basically all facts (imo). Could the state of prior art improve? 100%. If anything is unclear about the status quo, that will not be improved by creating a new place to store the same information.
> With that in mind, lets distill the core problem Corepack aims to resolve (relevant I swear):
> > Developers have many projects which use many different package managers & versions on their machines & run into problems when they use the wrong package manager or version for their projects.
> Lets distill the core problem a new "node version manager" would aim to resolve:
> > Developers have many projects which use many different node.js versions on their machines & run into problems when they use the wrong node.js version for their projects.
> Kind-of specific, so lets take a step back because we know node.js isn't the only "runtime". What would a "runtime manager" aim to resolve:
> > Developers have many projects which use many different runtimes & versions on their machines & run into problems when they use the wrong runtime or version for their projects.
> Feeling like there's some similarities here...
> Let's distill the core problem npm aims to resolve:
> > Developers have many projects which use many different dependencies & versions on their machines & run into problems when they use the wrong dependencies or version for their projects.
> Conjecture(s):
> 1. A runtime is a dependency
> 2. A package manager is a dependency
> 3. Developers want to manage their dependencies the same way
> Question(s):
> 1. How do we add value creating a tool to manage a subset of developer's dependencies? (ie. does that not compete with conjecture #3)
> 2. How is this different then the existing, default, dependency manager? (ie. npm)


**@styfle**:

> 1. User defines expected package manager and version in a canonical location such as package.json
> 2. Any user/CI/CD/etc that runs the package manager automatically installs the selected version prior to running <pkgmgr> install
> 3. When cloning a repo, you should never see a mismatch lockfile because the same version was used each time
> 4. When running in CI/CD, regardless of platform, you should never have a failed build due to mismatch package manager

