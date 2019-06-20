# Baseline practice - Document support levels

Package maintainers provide different level of support in the large npm ecosystem.
A mismatch between the support a maintainer is planning to
provide and that expected by a consumer of a module will cause
friction and stress on both the package maintainer and
the consumer. This is further complicated because the level of support
provided for dependencies of a package may be different than that
targeted by the package a consumer is directly consuming.

This baseline practice suggests a standardized set of information to
quantify the level of support that a package maintainer wishes/is able to
provide. The goal is to close the gap between the expectations from the
consumer and those of the maintainer and reduce the friction and stress
that can arise due to the gap.

There are 4 main dimensions that we standardize in this practice which are:  

* `target`: the level of support that the package maintainer aims to provide
* `response`: how quickly the maintainer chooses to, or is able to, respond to issues
* `response-paid`: how quickly the maintainer will respond to issues if paid
* `backing`: how the project is supported

In addition a `url` field can optionally be provided with a link to more detailed
support information.

For each of these dimensions the potential options are not an ordered list.
Instead like licenses each ID will identify a unique option. If you wish to
identify your package with an option which is not yet listed, please PR your
option into the lists in the sections which follow. 
The values can be any string, those which are not documented in the lists within
this document considered "custom" and may ignored for flagged by any tooling that
consumes these elements.

## Support file

The support informations are stored in a `support.json` file 
The recommended baseline practice is to include a file named `support.json` in the root direcotry of the project.

This file documents the maintainers expectations adding more useful metadata.

The file expects this example structure:

A `support` field with a `versions` key.
`versions` is an array of JSON that contains all the useful information detailed below.

```json
{
  "support": {
    "versions": [
      {
        "version": "^1.0.0",
        "target": "abandoned",
        "response": "none",
        "response-paid": "regular-1",
        "backing": [
          "paid-support",
          "sponsored"
        ],
        "expires": "2019-08-01T20:47:27.840Z",
        "contact": {
          "url": "http://support.it/issue",
          "security": "mailto:security@nodejs.com",
          "paid-channel": "mailto:iwantmoney@nodejs.com"
        },
        "funding": {
          "open-collective": "",
          "btc": ""
        }
      },
      {
        "version": ">=2.0.0",
        "target": "lts",
        "response": "regular-7",
        "response-paid": "regular-1",
        "backing": "hobby",
        "expires": "2021-08-01T20:47:27.840Z",
        "contact": {
          "url": "http://support.it/issue",
          "security": "mailto:security@nodejs.com",
          "paid-channel": "mailto:iwantmoney@nodejs.com"
        },
        "funding": {
          "open-collective": "",
          "btc": ""
        }
      }
    ]
  }
}
```

Note that the `version` ranges could overlap each other: it means that the maintainers provide more
than one support type, and it is up to users choose the support level that best fits their need.

The default for packages created by individuals for their own use should most often be:

```json
{
  "support": {
    "versions": [
      {
        "version": "*",
        "target": "lts",
        "response": "best-effort",
        "backing": [
          "hobby",
          "sponsored"
        ],
        "expires": "2019-08-01T20:47:27.840Z",
        "contact": {
          "url": "https://github.com/nodejs/package-maintenance/issues",
          "security": "mailto:security@nodejs.com"
        }
      }
    ]
  }
}
```

This reflects that the maintainer in this case may have no interest in ensuring that the package works
outside of their use case.


## Support `version`

The support version accepts a [semver range](https://semver.io/) value that define the versions of the
module that applies that configuration.


## Support `target`

The support target captures the level of support that the package maintainer
aims to provide.  The standardized options are as follows:

| Value | Description |
|-------|-------------|
| `abandoned`  | Not recommended for use. The package is deprecated or no longer maintained.
| `none`       | Use at your own risk, no active support. May or may not work for a given Node.js version.
| `latest`     | The package is maintained only for the Latest Node.js versions. You will be required to update to the latest LTS Node.js version in order to ensure you can use new versions/get security fixes.
| `lts`        | The package is maintained for the Node.js LTS releases (both in Active and Maintenence mode). Anyone creating an application using an LTS version of Node.js and using the latest major version of LTS adopting modules will not have to accept semver-major level (ie. breaking) changes into that application in order to receive essential fixes. Full details are available [here](https://github.com/nodejs/package-maintenance/issues/119) (should we bring this into the package-maintenance repo?)
| `superset`   | The package is maintained for versions of Node.js including both LTS and non-LTS releases. It may be necessary to accept semver-major level (ie. breaking) changes into that application in order to receive essential fixes. Documentation for the package will include the non-LTS releases for which the package is still maintained. 

As an example based on the current active Node.js releases which are 6.x, 8.x, 10.x (LTS) and 11.x (Current)
support would be as follows where X indicates support is provided:

| Support-target| 6.x | 8.x | 10.x | 11.x | Others as documented  |
|---------------|-----|-----|------|------|-----------------------|
| `abandoned`   |     |     |      |      |                       |
| `none`        |     |     |      |      |                       |
| `latest`      |     |     |   X  |      |                       |
| `lts`         |  X  |  X  |   X  |      |                       |
| `superset`    |  X  |  X  |   X  |   X  |           X           |


## Support `response` and `response-paid`

Support response quantifies how quickly the maintainer chooses to, or is able to, respond to issues:

| Value | Description |
|-------|-------------|
| `none`         | Don't expect a response, the package is not being actively maintained
| `best-effort`  | The maintainer is interested in fixing/discussing issues, however, there should be no expectation on response times. If and when the maintainer has time they may respond.
| `regular-7`    | There are dedicated resources who regularly maintain the module, expected response time is 7 days or less for a "we read your issue" response. Further work will depend on prioritization of the issue by the maintainer team.
| `regular-1`    | There are dedicated resources who regularly maintain the module, expected response time is 1 days or less for a "we read your issue" response. Further work will depend on prioritization of the issue by the maintainer team.
| `24-7`         | There are dedicated resources who regularly maintain the module and they are available 24/7. You can expect to be able to contact the maintainers and get an initial response with 6 hours.

Support-response indicates the expectation unless you have paid one of the maintainers or a company that provides
3rd party support. If paid support is available then Support-response-paid is an array of one or more options listing the
options that the maintainer knows are available.


## Support `backing`

This section can be a single value or an array of values, for example: [x, y, z]. This supports cases where the
backing comes from more than one source. The documented options include:

| Value | Description |
|-------|-------------|
| `none`         | There is nobody backing this module
| `hobby`        | The single maintainer maintains the package for fun, does not get any support to continue maintenance.
| `sponsored`    | The single maintainer actively maintains the package but depends on sponsorship to be able to continue to maintain the package. Consider supporting this sponsorship through patreon etc.
| `bounty`       | The package is maintained through the use of a bounty service
| `project`      | The package is maintained under the auspices of a larger project (ex Node.js project).
| `foundation`   | The package is maintained and supported under the auspices of a Foundation.
| `company`      | The package is maintained and supported by a corporate entity but may not be related to their product or service offerings.
| `commercial`   | The package is maintained and supported by a corporate entity as part of supporting their products.
| `paid-support` | The package is maintained and supported through paid support contracts.
| `freemium`     | Basic version of the package it provided for free, premium version is available at a cost.


## Support `expires`

The expire field is a string in ISO Date format which define the ending of the term of that support entry.


## Support `contact`

The contact field is a JSON that show to users all the possible channels to contact the maintainer:

```json
"contact": {
  "url": "http://support.it/issue", // URL to the issues tracker
  "security": "mailto:security@nodejs.com", // A contact for security issues
  "paid-channel": "mailto:iwantmoney@nodejs.com" // A direct contact for paid support
},
```


## Support `funding`

This field should track all the possibilities to fund the project to receive a paid support.

```json
"funding": {
  "open-collective": "",
  "btc": ""
}
```
