# Publishing packages

## What?

These are guidelines for publishing packages to the npm registry.

## Why?

After you publish your package to the public npm registry, it's visible to everyone on the internet and your users will install your package into their `node_modules`.  There are a few reasons that keeping your published package tidy:

- Security - avoid accidentally publishing your credential files like keys
- Tidiness - avoid publishing non essential temp files like `.nyc_output` or `coverage`

## How?

These guidelines exist to help package owners with some practices on managing packages for publishing.  The primary focus is about filtering files that are published, but there are other helpful related resources as well.

### Overview

[npm] maintains a public registry for everyone to publish packages.  Here are some related resources:

| Purpose                        | How                         | comment                                                   |
| ------------------------------ | --------------------------- | --------------------------------------------------------- |
| bump version                   | [`npm version`]             | This bumps version and creates git commit and tag for you |
| preview/view tarball           | [`npm pack`]                | Allows you to see files before or after publishing        |
| publish config                 | [`publishConfig`]           | Helpful if you need to publish to a different registry    |
| publish package                | [`npm publish`]             | Actually publish the package                              |
| search/view published packages | [public registry]           | [for example](https://www.npmjs.com/package/npm)          |
| filter publish files           | [`.npmignore`] or [`files`] | Use one base on your preference                           |

### `.npmignore` or `files`

[npm] has default ignore rules and loads from `.gitignore` but it also offer two methods for you to keep your published packages tidy.

- blacklisting - specifying ignore files in `.npmignore`
- whitelisting - specifying files you only want to publish with `files` in your `package.json`.

Which one to go with is solely up to you and your preference, but beware of the following gotchas and tips:

On the `.gitignore` file:

- [npm] automatically uses `.gitignore` if neither one exist

On the `.npmignore` file:

- using `.npmignore`, you could potentially publish any unintended files left in the directory.
- [npm] will stop using `.gitignore` if this exists, so beware because you may forget to add some rules to `.npmignore` after you add them to `.gitignore`

On the `files` field in `package.json`:

- the opposite of `.npmignore`, if you forget to add some new files to this, you could publish a package that's broken because of missing files.
- there's an open bug that [`files` affects npm's default rules](https://npm.community/t/ds-store-files-show-up-after-npm-publish/831/4)
  - The result is npm's default ignore rules has no effect on files under directories that are whitelisted by `files`.
  - For example, if you set `"files": [ "lib" ]`, then `lib/.gitignore` will be published and there's no easy way to avoid that.

### Verifications

Run `npm publish --dry-run` to check what you are about to publish first.  In the newer [npm] version 6, [`npm publish`] now shows the list of files so you can inspect that also.

You can use the [`npm pack`] command to generate a tarball to see exactly what will be uploaded to the registry.

You can also use the [`npm pack`] command to download a tarball from a published version.

For example: `npm pack npm@6.5.0`.

### Transpiling Sources

A package written in another language like TypeScript should be published with transpiled JavaScript as the primary executable.

Generally the original sources should not be required to use your published package, but it's your preference whether to publish them or not.

### Publish and Install scripts

If your package requires any build steps such as transpiling sources, then note that [npm's recommendation](https://docs.npmjs.com/misc/scripts#best-practices) is to run those before you publish, not when your user install your package.

The [npm scripts] `prepare` and `prepublishOnly` are intended for this purpose.

### Tests and Docs

For your tests and extra docs, it's your preference on whether to publish them or not.

Keep in mind that tests generally are more relaxed at what they are allowed to do and easier to overlook, so they are a location where someone could potentially hide malicious code to cause harm.

### Other Resources

There are tools that help you with the verification and publishing process:

- https://www.npmjs.com/package/publish-please


[npm]: https://www.npmjs.com/
[`npm version`]: https://docs.npmjs.com/cli/version
[`npm publish`]: https://docs.npmjs.com/cli/publish
[`npm pack`]: https://docs.npmjs.com/cli/pack
[`publishConfig`]: https://docs.npmjs.com/files/package.json#publishconfig
[public registry]: https://www.npmjs.com/
[`.npmignore`]: https://docs.npmjs.com/misc/developers#keeping-files-out-of-your-package
[`files`]: https://docs.npmjs.com/files/package.json#files
[npm scripts]: https://docs.npmjs.com/misc/scripts#description
