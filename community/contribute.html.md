```
title: Contributing
```


## Donations

With your help, we'll be able to work on DocPad full time! Isn't that awesome? [Donate now to let that happen!](/donate)


## Publicize

Help spread the word of DocPad:

- Star our [GitHub Repository](https://github.com/bevry/docpad) by clicking the "Star" button on the top right
- Star our [NPM Package](https://npmjs.org/package/docpad) by running `npm star docpad` in your terminal
- Join our [DocPad Gittip Community](/gittip-community)
- Join our [DocPad Google+ Community](/google+)
- Talk about us on Social Media; Twitter, Blogging, etc.
- Write about your experiences of DocPad on your blog
- Do a short less than a minute video testimonial of DocPad on Youtube!
- And just continue to be awesome


## Skeletons

To add a new skeleton to the skeleton listing:

1. Add your new skeleton to our [`exchange.json` file](https://github.com/bevry/docpad-extras/edit/docpad-6.x/exchange.json)
1. Submit the pull request for it (the page for this should appear automatically once you click "Commit Changes" from the previous link)


## Documentation

To update our documentation:

1. Our documentation is located at the [`docpad/documentation` repository](https://github.com/docpad/documentation)
1. We have [strict documentation criteria](http://learn.bevry.me/community/documentation-guidelines) that all documentation changes must abide by
1. You can edit a file by opening that file in the repository browser, and then clicking the "Edit" button
1. Once done, click save changes or whatever the button says and this will then take you to a "Submit Pull Request" page
1. Fill in the details and click submit


## Coding Standards

Follow the [Bevry Coding Standards](http://learn.bevry.me/community/coding-standards) when writing your changes


## Setup

To get started with developing and contributing code, you must first setup your project for development.


### Setup the DocPad core for development

To setup a development environment for contributing to the DocPad core follow these steps:

1. Install CoffeeScript globally: `npm install -g coffee-script` (may require `sudo` access)
1. Fork the repository of the DocPad Core: https://github.com/bevry/docpad
1. Clone your fork to your machine then `cd` into it
1. Run `npm install` to install any missing dependencies
1. Run `cake compile` to compile the project (or use `cake watch` to compile every time a change is made)
1. Run `cake test` to test the project
1. Run `npm link` to make this development instance of the projects available to other projects (via `npm link docpad`)


### Setup a DocPad plugin for development

To setup a development environment for contributing to a plugin follow these steps:

1. Ensure you have DocPad setup for development, by running the DocPad core instructions above
1. Fork the repository of the DocPad plugin you wish to edit
1. Clone your fork to your machine then `cd` into it
1. Run `npm link docpad` to link our local development instance of DocPad that we setup earlier to our DocPad plugin
1. Run `cake install` to install any missing dependencies
1. Run `cake compile` to compile the project (or use `cake watch` to compile everytime a change is made)
1. Run `cake test` to test the project
1. Run `npm link` to make this development instance of the project available to other projects (via `npm link docpad-plugin-PLUGINNAME`)


## Publishing

Follow these steps in order to implement your changes/improvements into the plugin or DocPad core.

### Preparation

1. Make sure your changes are on their own branch that is branched off from master
    1. You can do this by: `git checkout master; git checkout -b your-new-branch`
    1. And push the changes up by: `git push origin your-new-branch`
1. Make sure all tests are passing: `cake test`
    1. If possible, add tests for your change, if you don't know how, mention this in your pull request
1. If the project has a prepublish step, run it: `cake prepublish` (if it doesn't have this step that command will fail)


### Testing the DocPad core against plugins

Before you submit changes to the DocPad core you'll want to make sure they don't break any of our officially supported plugins:

1. Clone the [`docpad-extras` repository](https://github.com/bevry/docpad-extras) and `cd` into it
1. Make your development DocPad instance available to the plugin runner (run `npm link docpad`)
1. Install the dependencies: `npm install`
1. Clone the plugins: `./app clone`
1. Test the plugins: `./app test`


### Pull Request

To send your changes for the project owner to merge in:

1. Submit your pull request
    1. When submitting, if the original project has a `dev` or `integrate` branch, use that as the target branch for your pull request instead of the default `master`
    1. By submitting a pull request you agree for your changes to have the same license as the original plugin


### Publish

To publish your changes as the project owner:

1. Switch to the master branch: `git checkout master`
1. Merge in the changes of the feature branch (if applicable)
1. Increment the version number in the `package.json` file according to the [semantic versioning](http://semver.org) standard, that is:
    1. `x.0.0` MAJOR version when you make incompatible API changes,
    1. `x.y.0` MINOR version when you add functionality in a backwards-compatible manner, and
    1. `x.y.z` PATCH version when you make backwards-compatible bug fixes.

1. Add an entry to the changelog following the format of the previous entries, an example of this is:

    ``` markdown
    - v6.29.0 April 1, 2013
        - Progress on [issue #474](https://github.com/bevry/docpad/issues/474)
        - DocPad will now set permissions based on the process's ability
            - Thanks to [Avi Deitcher](https://github.com/deitch), [Stephan Lough](https://github.com/stephanlough) for [issue #165](https://github.com/bevry/docpad/issues/165)
        - Updated dependencies
    ```


1. Commit the changes with the commit title set to something like `v6.29.0. Bugfix. Improvement.` and commit description set to the changelog entry
1. Use `cake publish`, which will publish the module to npm, create a Git tag for it, push your master changes and new tags up to origin
    1. When prompted for your Git tag annotation (your text editor will open up automatically), enter the changelog entry, save the prompted file, and close the file

And that's it. :)
