# Publishing Clean npm Packages

## Introduction

In the node.js package maintainence working group, one of the topics we've been discussing is about publishing clean npm packages that do not include extra meta files.

The meta files are either OS specific or config files for the development tools used for the package.

Some common meta files are:

- `coverage`, `.nyc_output` - coverage output for istanbul and nyc
- `.idea`, `.vscode`, `.editorconfig` - configs for IDE or editors
- `.eslintrc`, `.babelrc`, `.prettierrc`, `nycrc`, `.jshintrc`, `.nvmrc`
- `.github`, `.travis.yml` - github and travis config directory
- `.npmignore` - npm publish ignore list file
- `.DS_Store` - Mac OS filesystem meta data

In our discussionm, we agreed that these files, while generally small, should not be part of a published package.

There were two things that we didn't have a conclusive agreement:

The first is how should package keep these files out when publishing.
The second is whether other files like tests and sources should be published.

## Publish without Meta Files

When publishing, npm allows you to either exclude certain files or include only the files you want. They work opposite of each other so you have to decide on the approach you want to take.

### Excluding Files

By default, npm uses exclusion to skip publishing files, and it actually comes with reasonable defaults to exclude some of the most common files like `.gitignore`. It automatically use `.gitignore` to exclude more files, but you can specify another file `.npmignore` instead - if `.npmignore` is present, `.gitignore` is ignored.

### Including Files

npm supports another way to skip publishing files through an include list in package.json. You can set a field `files` with an array of files that npm should only include in your published packages.

By default, npm also has some reasonable included files, like package.json, README.md, and LICENSE, and some reasonable excluded files, like package-lock.json, that you can not override.

### Exclude or Include

Since the two approaches are completely opposite of each other, there are different reasons to pick one over the other.

The main one revolves around new files you may add to your package.

With exclusion, new files are still published automatically, but with inclusion, you may end up publishing a broken package because you forgot to include the new files.

There are two counter reasons for if you want to use inclusion instead.

First, you may create new temporary files that are not intended to be published. There have been known incidents of packages being published with huge temp files accidentally. The downside of this is debatable, because the package still works perfectly.

Second, the include list allows specifying a directory where all files under it are all automatically included.

In the end, given that both ways are well supported by npm, we agreed to leave the choice to package authors.

Regardless of which one you pick, if you publish packages to npm, then you should use the `--dry-run` npm option to preview the files before publishing - or even better, enable 2FA, and the publish process will print out a list of files to be published before pausing to await your 2FA code.

## Tests and Sources

If you look at the packages installed in your `node_modules`, you would see that most of them have their tests with them also.

If a package's original code is written in another language like TypeScript, then they would have transpiled code for consumption, but the original sources are published also.

As a user, it's most likely you don't need the tests and the sources to consume a package, so it's a waste that you have to download and install them when you just want to use the package in your code.

That raises the question: should you publish your tests and sources as part of your package?

It turns out there are two camps of opinions on this, and we found ourselves split on both sides of the fence.

Both sides have good reasons. Published packages are immutable and more permanent than if they were on github.com so it's a good thing if we can download them run a version's tests if we want to. On the other hand, they use up bandwidth and disk space.

There are multiple paths that we explored for this.

First one is to allow publishing a package in multiple parts like production and development. This requires significant support from npm so it's just an idea.

Alternatively, we are looking into creating tools for cleaning up your `node_modules`.

Finally, the tink project should make this a non issue because it only brings the files your application needed on demand.

## Closing

We established a baseline and a recommendation guide for publishing packages without meta files, using either the exclude or include support from npm.

The original github issue and comments can be found here https://github.com/nodejs/package-maintenance/issues/164.

We consider the options for publishing tests and sources. While we look forward to the tink project that will handle this better, we are exploring interim solutions to trim some fats from `node_modules`.
