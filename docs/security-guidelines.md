## What

Guidelines for responsible reporting and disclosure of security vulnerabilities.

## Why

Defining a process of reporting and disclosing security vulnerabilities helps maintainers protect projects and their users.

## Security policy guidelines

### Publishing the policy

Each project should document its security policy in an easily accessible place.

The recommended approach is to [publish security policy in a GitHub repository](https://help.github.com/en/github/managing-security-vulnerabilities/adding-a-security-policy-to-your-repository).

Here are several alternative ways of publishing security policies:

1. `SECURITY.md` or `SECURITY` file in the root folder of project repository (if hosted outside of GitHub).
1. Security page on project website, e.g. `https://nodejs.org/en/security/`.
1. [security.txt](https://securitytxt.org/) file on project website, e.g. `https://nodejs.org/.well-known/security.txt`.
1. Security section of the project `README` file.

A project's public issue tracker should point out that security issues need to be kept private initially.
If using GitHub issues, mention in the [issue template](https://help.github.com/en/github/building-a-strong-community/configuring-issue-templates-for-your-repository#creating-issue-templates)
that there is a separate process for security-sensitive issues.  If using a vulnerability rewards program,
the public issue tracker advice should make it clear what is in bounds.

### Reporting a security issue

Project security policy should describe a process for reporting vulnerabilities. It is strongly encouraged that the reporting process is confidential to allow maintainers to triage and resolve the vulnerability in private before disclosing it to the public.

A common way of reporting vulnerabilities is through a designated email address, e.g. `security@example.com`.

The policy should clearly specify when confidential reporting is not supported and generally available bug tracking system should be used.

### Responsible disclosure

Public disclosure should follow release of a patch that addresses a vulnerability.

The recommended approach is to [create a maintainer advisory on GitHub](https://help.github.com/en/github/managing-security-vulnerabilities/creating-a-maintainer-security-advisory).

Here are several alternative ways to disclose a vulnerability:

1. [Report a vulnerability to npm](https://docs.npmjs.com/reporting-malware-in-an-npm-package).
1. Submit a pull request to [vulnerability database](https://github.com/nodejs/security-wg/blob/master/processes/vuln_db.md) maintained by [Node.js Ecosystem Security WG](https://github.com/nodejs/security-wg).

### Collaboration between maintainers and reporters

The policy should recommend that maintainers and reporters collaborate to ensure the accuracy of the vulnerability report and the security advisory. In particular, information such as: 

1. Severity (e.g. CVSS score)
1. Category (e.g. CWE category)
1. Exact package that is vulnerable
1. Affected versions
1. Vulnerability impact

should be established in collaboration between maintainers and the reporter.

If possible, the policy should recommend means of communication between all parties working towards responsible disclosure. See [Maintainer advisories on GitHub](https://help.github.com/en/github/managing-security-vulnerabilities/creating-a-maintainer-security-advisory)

### Releasing security patches

If releasing security patches deviates from the standard package release process, it should be clearly stated in the security policy.

In particular, if package maintainers cannot commit to releasing security patches in a timely fashion, it should be noted explicitly to allow package consumers to make an informed decision about using the package based on their risk tolerance.

## Examples

Here are several examples of short and useful security policies that fit different maintainers' needs:

| Template | Description |
| -------- | ----------- |
| [Node.js Ecosystem Security WG Template](https://github.com/nodejs/security-wg/blob/master/processes/responsible_disclosure_template.md) | The common security policy that all packages may follow |
| [Express Security Policies and Procedures](https://github.com/expressjs/express/security/policy) | Supports a customized workflow and the Node.js Ecosystem Security WG reporting vulnerabilities process |
| [Node-RED Security Policy](https://github.com/node-red/node-red/security/policy) | Defines a dedicated security reporting workflow |
| [Fastify Security Policy](https://github.com/fastify/fastify/blob/master/SECURITY.md) | Adopt the Node.js Ecosystem Security WG reporting vulnerabilities process |
| [Node.js Issue Template](https://github.com/nodejs/node/issues/new/choose) | Uses issue templates to guide vulnerability reporters away from the public issue tracker. |
| [Google VRP Bounds](https://www.google.com/about/appsecurity/reward-program/#vulns) | Explains to security researches what is in bounds for a vulnerability rewards program. |
