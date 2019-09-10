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
For the JavaScript ecosystem it is recommended that this information be added to the existing
`package.json` file in the root directory of the project. For other ecosystems, it is recommended that
this information be stored in a file called `package-support.json` in the root directory of the 
project.

The json which is either added to the `package.json` file or stored in `package-support.json` is
as defined in the sections below.  

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
          "type": "ad-hoc",
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

| Value         | example    | Description |
|---------------|------------|-------------|
| xxxxxx        |            | where xxxxxx is a [semver range](https://semver.io/) of Node.js versions supported.
| `abandoned`   |            | Not recommended for use. The package is deprecated or no longer maintained
| `none`        |            | Use at your own risk, no active support. May or may not work for a given Node.js version
| `all`         | 8,10,11,12 | The package is maintained for versions of Node.js including both LTS and non-LTS releases. It may be necessary to accept semver-major level (ie. breaking) changes into that application in order to receive essential fixes. Documentation for the package will include the non-LTS releases for which the package is still maintained. 
| `lts`         | 8,10       | The package is maintained for the Node.js LTS releases (both in Active and Maintenence mode). Anyone creating an application using an LTS version of Node.js and using the latest major version of LTS adopting packages will not have to accept semver-major level (ie. breaking) changes into that application in order to receive essential fixes. Full details are available [here](https://github.com/nodejs/package-maintenance/issues/119)
| `active`      | 10,12      | All releases not in maintenance
| `lts_active`  | 10         | All releases both LTS and active
| `lts_latest`  | 10         | The package is maintained only for the Latest Node.js version. You will be required to update to the latest LTS Node.js version in order to ensure you can use new versions/get security fixes
| `maintained`  | 12,10,8    | Node.js versions which are not EOL
| `current`     | 12         | The latest release from "all"

Based on the current active Node.js releases which are 8.x (Maintenance LTS), 10.x (Active LTS) and 12.x (Current).

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
    "type": "ad-hoc",
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
| `none`         | Don't expect a response, the package is not being actively maintained
| `ad-hoc`       | The maintainer is interested in fixing/discussing issues. However, there should be no expectation on response times. If and when the maintainer has time, they may respond.
| `regular-X`    | There are dedicated resources who regularly maintain the package, expected response time is X days or less for a "we read your issue" response. Further work will depend on prioritization of the issue by the maintainer team.
| `24-7`         | There are dedicated resources who regularly maintain the package and they are available 24/7. You can expect to be able to contact the maintainers and get an initial response with 6 hours.

### Support `backing`

This section provides information how the package is supported and how consumers can help support the package.
It can be a single object or an array of objects, for example: [x, y, z]. This supports cases where the
backing comes from more than one source. Each object consists of an identifier as defined below and an optional URL with additional information. For example:

```json
{ "foundation": "https://openjsf.org/" }
```

The value can be an array of URLs as well:

```json
{
  "sponsored": [
    "https://opencollective.com/my-account",
    "https://www.patreon.com/my-account",
    "https://tidelift.com/subscription/pkg/my-package"
  ]
}
```

This allows the package maintainer to indentify how the packge is supported as well as provide links to additional information for how a consumer may find more information or help support the package.

The standardized identifiers include:

| Value | Description |
|-------|-------------|
| `none`         | There is nobody backing this package
| `hobby`        | The single maintainer maintains the package for fun, does not get any support to continue maintenance.
| `sponsored`    | The single maintainer actively maintains the package but depends on sponsorship to be able to continue to maintain the package. Consider supporting this sponsorship through the funding platforms listed.
| `bounty`       | The package is maintained through the use of a bounty service
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
