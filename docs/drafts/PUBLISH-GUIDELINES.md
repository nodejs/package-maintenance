# What?

This is guidelines for publishing packages to the npm registry.

# Why?

After you publish your package to the public npm registry, it's visible to everyone on the internet and your users will install your package into their `node_modules`.  There are a few reasons that keeping your published package tidy:

- Security - avoid accidentally publishing your credential files like keys
- Tidiness - avoid publishing non essential temp files like `.nyc_output` or `coverage`

# How?

These guidelines exist to help package owners with some practices on managing packages for publishing.  The primary focus is about filtering files that are published, but there are other helpful related resources as well.

## Overview

[npm] maintains a public registry for everyone to publish packages.  Here are some related resources:

| Purpose                        | How                         | comment                                                   |
| ------------------------------ | --------------------------- | --------------------------------------------------------- |
| bump version                   | [`npm version`]             | This bumps version and creates git commit and tag for you |
| preview/view tarball           | [`npm pack`]                | Allows you to see files before or after publishing        |
| publish config                 | [`publishConfig`]           | Helpful if you need to publish to a different registry    |
| publish package                | [`npm publish`]             | Actually publish the package                              |
| search/view published packages | [public registry]           | [for example](https://www.npmjs.com/package/npm)          |
| filter publish files           | [`.npmignore`] or [`files`] | Use one base on your preference                           |

## `.npmignore` or `files`

[npm] has default ignore rules and loads from `.gitignore` but it also offer two methods for you to keep your published packages tidy.

- blacklisting - specifying ignore files in `.npmignore`
- whitelisting - specifying files you only want to publish with `files` in your `package.json`.

Which one to go with is solely up to you and your preference, but beware of the following gotchas and tips:

On the `.gititnore` file:

- [npm] automatically uses `.gitignore` if neither one exist

On the `.npmignore` file:

- using `.npmignore`, you could potentially publish any unintended files left in the directory.
- [npm] will stop using `.gitnore` if this exists, so beware because you may forget to add some rules to `.npmignore` after you add them to `.gitignore`

On the `files` field in `package.json`:

- the opposite of `.npmignore`, if you forget to add some new files to this, you could publish a package that's broken because of missing files.
- there's an open bug that [`files` affects npm's default rules](https://npm.community/t/ds-store-files-show-up-after-npm-publish/831/4)

## Verification

In the newer [npm] version 6, [`npm publish`] now shows the list of files published, but it doesn't offer you a chance to review them first.

If you want to review the files, you can use the [`npm pack`] command to generate a tarball first and look inside it.

You can also use the [`npm pack`] command to download a tarball from a published version.

For example: `npm pack npm@6.5.0`.

## Sources, Tests, and Docs

A package not written in idiomatic JavaScript should be published with transpiled JavaScript as the primary executable.

If you write your package in another language like TypeScript and you have other files like tests and extra docs, then it's your preference on whether to publish them or not.

Keep in mind that tests is a location where someone could potentially hide malicious code to cause harm.

## Other Resources

There are tools that help you with the verication and publishing process:

- https://www.npmjs.com/package/publish-please


[npm]: https://www.npmjs.com/
[`npm version`]: https://docs.npmjs.com/cli/version
[`npm publish`]: https://docs.npmjs.com/cli/publish
[`npm pack`]: https://docs.npmjs.com/cli/pack
[`publishConfig`]: https://docs.npmjs.com/files/package.json#publishconfig
[public registry]: https://www.npmjs.com/
[`.npmignore`]: https://docs.npmjs.com/misc/developers#keeping-files-out-of-your-package
[`files`]: https://docs.npmjs.com/files/package.json#files
