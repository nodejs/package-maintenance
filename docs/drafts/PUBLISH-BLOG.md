# Publishing npm Packages

## Introduction

In the node.js package maintenance working group, one of the topics we've been discussing is about what files to include or exclude when publishing npm packages.

In general, a package's original directory could contain other meta files that may or may not be needed in published form. These files are either OS specific or config files for the development tools used for the package.

Some common meta files are:

- `coverage`, `.nyc_output` - coverage output for istanbul and nyc
- `.idea`, `.vscode` - configs for IDE or editors
- `.github`, `.travis.yml` - github and travis config directory
- `.npmignore` - npm publish ignore list file
- `.DS_Store` - Mac OS filesystem meta data

In our discussion, we agreed that these files, while generally small, should not be part of a published package.

There were two things that we didn't have conclusive agreement on:

1. how packages should exclude these files when publishing
1. whether other files like tests and sources should be published (but would be a non-issue once npm tink project is released)

## Publish without Meta Files

When publishing, npm allows you to either exclude certain files or include only the files you want. They work opposite of each other so you have to decide on the approach you want to take.

### Excluding Files

By default, npm uses exclusion to skip publishing files, and it actually comes with reasonable defaults to exclude some of the most common files like `.gitignore`. It automatically uses `.gitignore` to exclude more files, but if another file `.npmignore` is present, then it will be used and `.gitignore` is ignored.

### Including Files

npm supports another way to skip publishing files through an include list in package.json. You can set a field [`files`](https://docs.npmjs.com/files/package.json#files) with an array of files and/or directories that npm should only include in your published packages.

npm also has some reasonable included files, like `package.json`, `README.md` and `LICENSE`, and some reasonable excluded files, like `package-lock.json`, that you cannot override.

### Exclude or Include

Since the two approaches are completely opposite of each other, there are different reasons to pick one over the other.

The main reason revolves around new files you may add to your package.

With exclusion, new files are still published automatically, but with inclusion, you may end up publishing a broken package because you forgot to include the new files.

There are two counter reasons for if you want to use inclusion instead.

First, you may create new temporary files that are not intended to be published. There have been known incidents of packages being published with huge temp files accidentally, which is an inconvenient nuance, but the package still works perfectly.

Some actual incidents found through github issues:

- https://github.com/STRML/async-limiter/issues/2
- https://github.com/wix/yoshi/pull/978
- https://github.com/bholloway/resolve-url-loader/issues/115

Second, the include list allows specifying a directory where all files under it are all automatically included.

In the end, given that both ways are well supported by npm, we agreed to leave the choice to package authors.

Regardless of which one you pick, if you publish packages to npm, then you should use the `--dry-run` npm option to preview the files before publishing. If you enabled 2FA, then you get an added benefit as a side effect where the publish process will print out a list of files to be published before pausing to await your 2FA code.

## Tests and Sources

If you look at the packages installed in your `node_modules`, you would see that most of them have their tests and rc files with them also.

If a package's original code is written in code that require transpilation to something like ES5, then the original source code probably is not needed but is sometimes still published.

As a user, you may not need the tests and the sources to consume a package. If so, they waste download bandwidth and disk space.

That raises the question: should you publish your tests and sources as part of your package?

It turns out there are two camps of opinions on this, and we found ourselves split on both sides of the fence.

Both sides have good reasons. Published packages are immutable and more permanent than if they were hosted on any public source control like github.com where there's no guarantee that the repo will never vanish, so it's a good thing if we can download from the registry a version's tests if we want to. On the other hand, they use up bandwidth and disk space for all installs.

There are multiple paths that we explored for this.

First one is to allow publishing a package in multiple parts like production and development. This requires significant support from npm so it's just an idea.

Alternatively, we are looking into creating tools for cleaning up your `node_modules`.

Finally, the tink project should make this a non issue because it only brings the files your application needed on demand.

npm tink project is particular exciting and will solve a lot of the issues we discussed here. Check it out at the following links; it's got a lot more to offer.

- [tink talk by Kat JSConfEU 2019](https://youtu.be/SHIci8-6_gs)
- [tink package on npm](https://www.npmjs.com/package/tink)
- [tink repo on github](https://github.com/npm/tink)

## Closing

We established a baseline and a recommendation guide for publishing packages without meta files, using either the exclude or include support from npm.

The original github issue and comments can be found here [package-maintenance/issues/164](https://github.com/nodejs/package-maintenance/issues/164).

We consider the options for publishing tests and sources. While we look forward to the tink project that will handle this better, we are exploring interim solutions to trim some fats from `node_modules`.
