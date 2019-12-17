## What

Guidelines for responsible reporting and disclosure of security vulnerabilities.

## Why

Defining a process of reporting and disclosing security vulnerabilities helps maintainers protect projects and their users.

## Security policy guidelines

### Publishing the policy

Each project should document its security policy in an easily accessible place.

Here are several common ways of publishing security policies:

1. [Security policy in a GitHub repository](https://help.github.com/en/github/managing-security-vulnerabilities/adding-a-security-policy-to-your-repository).
1. `SECURITY.md` or `SECURITY` file in the root folder of project repository (if hosted outside of GitHub).
1. Security section on project website, e.g. `https://example.com/security`.
1. [security.txt](https://securitytxt.org/) file on project website.
1. Security section of the project `README` file.

### Reporting a security issue

Project security policy should describe a process for reporting vulnerabilities. It is strongly encouraged that the reporting process is confidential to allow maintainers to triage and resolve the vulnerability in private before disclosing it to the public.

Here are several common ways of reporting vulnerabilities:

1. Designated email address, e.g. `security@example.com`.
1. [Node.js Ecosystem Security WG](https://github.com/nodejs/security-wg) responsible disclosure program on [HackerOne](https://hackerone.com/nodejs-ecosystem).

The policy should clearly specify when confidential reporting is not supported and generally available bug tracking system should be used.

### Responsible disclosure

Public disclosure should follow release of a patch that addresses a vulnerability.

Here are the recommended ways to disclose a vulnerability:

1. [Create a maintainer advisory on GitHub](https://help.github.com/en/github/managing-security-vulnerabilities/creating-a-maintainer-security-advisory).
1. [Report a vulnerability to npm](https://www.npmjs.com/advisories/report).
1. Submit a pull request to [vulnerability database](https://github.com/nodejs/security-wg/blob/master/processes/vuln_db.md) maintained by [Node.js Ecosystem Security WG](https://github.com/nodejs/security-wg).

Note that vulnerabilities reported to the responsible disclosure program on [HackerOne](https://hackerone.com/nodejs-ecosystem) will be automatically disclosed by HackerOne staff and the Ecosystem Security WG triage team members.

### Releasing security patches

If releasing security patches deviates from the standard package release process, it should be clearly stated in the security policy. In particular, if package maintainers cannot commit to releasing security patches in a timely fashion, it should be noted explicitly to allow package consumers to make an informed decision about using the package based on their risk tolerance.

## Examples

Here are several examples of short and useful security policies that fit different maintainers' needs:

- [Node.js Ecosystem Security WG Template](https://github.com/nodejs/security-wg/blob/master/processes/responsible_disclosure_template.md): the common security policy that all packages may follow
- [Express Security Policies and Procedures](https://github.com/expressjs/express/security/policy): support a customized workflow and the Node.js Ecosystem Security process
- [Node-RED Security Policy](https://github.com/node-red/node-red/security/policy): has defined a dedicated security reporting workflow
- [Fastify Security Policy](https://github.com/fastify/fastify/blob/master/SECURITY.md): adopt the Node.js Ecosystem Security WG process for reporting vulnerabilities
