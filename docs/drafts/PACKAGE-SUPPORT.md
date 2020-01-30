# Baseline practice - Document support levels

Package maintainers, in a wide variety of ecosystems, provide different
levels of support. A mismatch between the support a maintainer is planning to
provide and that expected by a consumer of a package will cause
friction and stress on both the package maintainer and
the consumer. This is further complicated because the level of support
provided for dependencies of a package may be different than that
targeted by the package a consumer is directly consuming.
In the case of JavaScript (node.js and browsers) there is a large ecosystem
of packages which are maintained in the `npm` registry and it is
this ecosystem in which we plan to test out this guidance. However, we
believe it will be applicable to other ecosystems and plan to make the
guidance generic enough to be applied in those ecosystems as well.

This baseline practice suggests a standardized set of information to
quantify the level of support that a package maintainer wishes/is able to
provide as well as information about how to access that support or to
support the package itself (for example by contributing to its funding).
The goal is to close the gap between the expectations from the
consumer and those of the maintainer and reduce the friction and stress
that can arise due to the gap.

There are 2 different aspects documented by this practice:

* Integration into packages
* Format and structure of the information 

The sections which follow will address each of these separately.

# Integration into packages

This recommendation is designed to meet the following
conflicting requirements:
* ability to review and process the support information
  offline with access to only the package itself.
* ability to update the support information without having to publish the module
* ability to get the most up to date version of the support info without
  having to pull down the latest published version of a package.

The integration suggested by this best practice aims to maximize the likelihood that
offline information is available and accurate while at the same time not tying
the canonical version of the support information with a published version of the
package.

## Integration into package.json

A new field called `support` is added to package.json. The contents of this field will 
be one of the following:
* true: This will indicate that the canonical version of the support information for the
  package is available in a file within the repository specified by the
  [repository](https://docs.npmjs.com/files/package.json#repository) entry.  In this case the filepath for the file containing the support information will be 
  `./package-support.json`
* a string: a relative path, starting with `./`, that points to a file within the
  repository specified in the [repository](https://docs.npmjs.com/files/package.json#repository)
  entry which contains the canonical support information. 
* object, with repository key matching the schema for the existing
  [repository](https://docs.npmjs.com/files/package.json#repository) entry, and optional
  path field that complies with the format described above under `a string`

These options allow the support information to be provided through a file:

* in the root of the repository for the package
* in a location other than the root in the repository for the package
* in a different repository from the package itself

and enable the following use cases:

1. most common case: `"support": true` with an associated `package-support.json` file in the
  package repo at the top level
1.less common case: an alternate file path within the package’s repo,
  such as `"support": "./path/to/support.json"`
1. least common case: sharing the same support data across multiple repos.
  Examples might be
  * `"support": { "repository": { "type": "git", "url": "https://github.com/nodejs/node-addon-api.git" }, "path": "support.json" }`
  * `”support”: { "repository": { "type": "git", "url": “https://github.com/nodejs/node-addon-api.git” } }`
  * `"support": { "repository": { "type": "git", "url": "https://github.com/nodejs/node-addon-api.git", "directory": "packages" }`

In all of these cases `package-support.json` (or your alternative filename) should be included in your `files`
array, or `.npmignore` configured to avoid excluding it.

The rationale for delivering the canonical version of the support info through a file
within a repository (and ideally the package's repository) is that it maximizes the likelihood
that every published package contains a copy of the support information that was
current at the time of the publish. Further, it does this in the most common cases without
requiring any special tooling or action from the maintainer.

In the least common case where the support information is not within the same repository,
we recommend that a non-canonical copy of the support information be copied into the package at the
same relative path as the external repository when publishing. We intend to work on tooling (including npm client) to simplify this 
process including validation of the path and content of the support information as well as the
required copying for the least common case.

Another benefit of delivering the support information from a repository is that existing
repositories (GitHub, GitLab, Bitbucket, etc.) provide a higher level of trust than
an unconstrained URL and tooling which pulls and processes the support information
can optionally limit where it will pull support information (along with the allowable
protocols like git, svn etc.) to a trusted set of repositories, increasing the
safety of running tools processing the support information.

The end result of this approach is that by default, each publish will contain a snapshot
of the support data, but the true source of truth is always a file within the package’s
repository (or within an external repository). This supports offline and
“no external internet” use cases as best as can be achieved.

In the future, we hope that the developer experience could be further improved
through itegration with the npm client. For validation could be integrated into
`npm publish`, and this information could be surfaced on npmjs.com, and/or the
information could be inlined into the packument so that `npm view $package`
could surface the data.

# Format and Structure

There are 3 main dimensions that we standardize in this practice which are:  

* `target`: the platform versions that the package maintainer aims to support. For example
  in the case of Node.js, the different versions of Node.js that the package supports.
* `response`: how quickly the maintainer chooses to, or is able to, respond to issues and
contacts for that level of support
* `backing`: how the project is supported

For each of these dimensions the potential options are not an ordered list.
Instead like licenses each ID will identify a unique option. If you wish to
identify your package with an option which is not yet listed, please PR your
option into the lists in the sections which follow. 
The values can be any string, those which are not documented in the lists within
this document considered "custom" and may ignored or flagged by any tooling that
consumes these elements.

## Support information

This field documents the maintainers’ expectations, adding more useful metadata.
For the JavaScript ecosystem it is recommended that this be provided as outlined in the
section titled `Integration into packages`. For other ecosystems, it is recommended that
this information be stored in a file called `package-support.json` in the root directory of the 
project.

The json is as defined in the sections below.  

The default for packages created by individuals for their own use should be:

```json
  "support": {
    "versions": [
      {
        "version": "*",
        "target": {
          "node": "none"
        },
        "response": {
          "type": "time-permitting",
          "paid": false,
          "contact": {
            "name": "Volunteers",
            "url": "https://github.com/myproject"
          }
        },
        "backing": {
          "hobby": "https://github.com/myproject"
        }
      }
    ]
  }
```

This reflects that the maintainer in this case may have no interest in ensuring that the package works
outside of their use case.

### Support `versions`

The `versions` key is an array of objects, each of which contains information for a package version
range. The standardized fields include:

* version
* target
* response
* backing
* expires

### Support `version`

The support version accepts a [semver range](https://semver.io/) value that define the versions of the
package that applies that configuration.

Note that the `version` ranges could overlap each other: it means that the maintainers provide more
than one support type, and it is up to users choose the support level that best fits their need.

### Support `target`

The support target captures the platform versions that the package maintainer aims to support.
These options may be different for each ecosystem so the target uses a namespace in 
order to identify which values are expected.

The target field is an object in this format:

{ "xxxx": [ ] }

where xxxx is the namespace identifier for the ecosystem and [ ] is either a string or an array
of strings indicating the platform versions that the package maintainer aims to support.

The standarized namespace identifiers are:

* "node"

#### node name space

The standardized options for the node name space are as follows:

| Value         | Current | Active LTS | Maintenance LTS | EOL | Example    | Description |
|---------------|---------|------------|-----------------|-----|------------|-------------|
| xxxxxx        |         |            |                 |     |            | xxxxxx is a [semver range](https://semver.io/) of Node.js versions supported
| `abandoned`   |         |            |                 |     |            | Not recommended for use. The package is deprecated or no longer maintained
| `none`        |         |            |                 |     |            | Use at your own risk, no active support. May or may not work for a given Node.js version
| `all`         |   ✔     |     ✔      |        ✔        |  ✔  | ...,8,9,10,11,12 | The package is maintained for versions of Node.js including both LTS and non-LTS releases regardless of whether they are EOL or not. It may be necessary to accept semver-major level (ie. breaking) changes into that application in order to receive essential fixes. Documentation for the package will include the non-LTS releases for which the package is still maintained (some maintainers support as far back as 0.6)
| `lts`         |         |     ✔      |        ✔        |     | 8,10       | The package is maintained for the Node.js LTS releases (both in Active and Maintenence status). Anyone creating an application using an LTS version of Node.js and using the latest major version of LTS adopting packages will not have to accept semver-major level (ie. breaking) changes into that application in order to receive essential fixes. Full details are available [here](https://github.com/CloudNativeJS/ModuleLTS)
| `active`      |   ✔     |     ✔      |                 |     | 10,12      | Current release and active LTS releases
| `lts_active`  |         |     ✔ (all)     |                 |     | 10         | All releases in _active_ LTS status. There may be more than one LTS release in active maintenance at a given point in time
| `lts_latest`  |         | ✔ (latest) |                 |     | 10         | The package is maintained only for the Latest LTS Node.js version. You will be required to update to the latest LTS Node.js version in order to ensure you can use new versions/get security fixes
| `supported`   |   ✔     |     ✔      |        ✔        |     | 12,10,8    | Node.js versions which are not EOL
| `current`     |   ✔     |            |                 |     | 12         | The latest release from "all"

The example above are based on the state of Node.js releases at the time of writing (2019-10-07)
which are: 8.x (Maintenance LTS), 10.x (Active LTS) and 12.x (Current).
Checkout the actual state in the [Release Schedule](https://github.com/nodejs/Release#release-schedule).

### Support `response` 

The support response field quantifies how quickly the maintainer chooses to, or is able to, respond to issues. This field can be a single object or an array of objects. Each object contains the following:

* type
* paid (optional)
* contact (optional)

The contact field is an optional object, or array of objects, which includes:
* name
* email (optional)
* url (optional)

Or you can shorten a given object into a single string with this format: `name <email> (url)`.

For example:

```json
response: [
  {
    "type": "time-permitting",
    "paid": false,
    "contact": {
      "name": "Volunteers",
      "url": "https://github.com/myproject"
    }
  },
  {
    "type": "regular-7",
    "paid": false,
    "contact": "John Foo <john@foo.com> (https://john.foo)"
  },
  {
    "type": "24-7",
    "paid": true,
    "contact": {
      "name": "xyz customer service",
      "email": "help@service.com",
      "url": "xyz.com/service"
    }
  },
  {
    "type": "regular-1",
    "paid": true,
    "contact": [
      "John Foo <john@foo.com> (https://john.foo)",
      {
        "name": "xyz customer service",
        "email": "help@service.com",
        "url": "xyz.com/service"
      }
    ]
  }
]
```

This allows the package maintainer to provide contact information for each of the support options that are available.

The standardized support identifiers are as follows:

| Value | Description |
|-------|-------------|
| `none`            | Don't expect a response, the package is not being actively maintained
| `time-permitting` | The maintainer is interested in fixing/discussing issues, however, there should be no expectation on response times. If and when the maintainer has time they may respond.
| `regular-X`       | There are dedicated resources who regularly maintain the package, expected response time is X days or less for a "we read your issue" response. Further work will depend on prioritization of the issue by the maintainer team.
| `24-7`            | There are dedicated resources who regularly maintain the package and they are available 24/7. You can expect to be able to contact the maintainers and get an initial response with 6 hours.

### Support `backing`

This section provides information how the package is supported and how consumers can help support the package.
It can be a single object or an array of objects, for example: [x, y, z]. This supports cases where the
backing comes from more than one source. Each object consists of an identifier as defined below and an optional URL (except for entries with type `npm-funding` which must have a value of `true`) with additional information. For example:

```json
{ "foundation": "https://openjsf.org/" }
```

The value can be an array of URLs as well:

```json
{
  "bounty": [
    "https://www.bountiesareus.com/my-account",
    "https://www.wepaybounties.com/my-account"
  ]
}

This allows the package maintainer to identify how the package is supported as well as provide links to additional information for how a consumer may find more information or help support the package.

The standardized identifiers include:

| Value | Description |
|-------|-------------|
| `none`         | There is nobody backing this package.
| `hobby`        | The single maintainer maintains the package for fun, does not get any support to continue maintenance.
| `npm-funding`  | The project is asking for funding and can be funded through the links provided in the `funding` field within the package.json.
| `bounty`       | The package is maintained through the use of a bounty service.
| `project`      | The package is maintained under the auspices of a larger project (ex Node.js project).
| `foundation`   | The package is maintained and supported under the auspices of a Foundation.
| `company`      | The package is maintained and supported by a corporate entity but may not be related to their product or service offerings.
| `commercial`   | The package is maintained and supported by a corporate entity as part of supporting their products.
| `paid-support` | The package is maintained and supported through paid support contracts.
| `freemium`     | Basic version of the package it provided for free, premium version is available at a cost.
| `donations`    | The project can be funded by any donations.


### Support `expires`

The expires field defines the the date range over which the support entry is/was valid.
It is a string in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format.

This standard can express:
+ _a date_ (ex: `2007-03-01T13:00:00Z`): the value is the expiring date. This value is strict and not dynamic.
+ _time range_ (ex: `2007-03-01T13:00:00Z/2008-05-11T15:30:00Z`): the value is the range of validity of the supported version. This value is strict and not dynamic.
+ _only duration_ (ex: `P1Y2M10DT2H30M`): the value must be added to the last release date. This value is dynamic.

To understand if the version is expired or not, the user needs to do the operation for _duration_:

`date of last release in the version range` **+** `expires value` **>** `now` => the support is not expired
`date of last release in the version range` **+** `expires value` **<** `now` => the support is expired

If no `expires` is specified, the support metadata will be considered invalid 2 years from the last published date. This ensures that
invalid or out of date data can only be present for up to 2 years.

## Publishing and Authoritative Version

If the support information is delievered as part of a package, leveraging the ecosystem's
existing package manager (as is recommended for the JavaScript ecosystem at this point),
the only way to update the support information is to publish a new version of the package.

Since an update to the support information does not affect code which consumes the
package a publish which updates only the support information can be considered SemVer
patch. You might consider minor or major versions if the support model is changing in a
material way to consumers of your package.

Managing this information via releases means that any version of the package except the latest
may outdated support information. In the JavaScript ecosystem this means the authoritative
version of support information is the `latest` tag from npm for a package.
