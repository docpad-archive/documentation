```
title: Contributing
```


## Donations

[With your help, we'll be able to work on DocPad full time! Isn't that awesome? Donate now to let that happen!](/donate)


## Publicize

Help spread the word of DocPad:

- Star our [GitHub Repository](https://github.com/bevry/docpad) by clicking the "Star" button on the top right
- Star our [NPM Package](https://npmjs.org/package/docpad) by running `npm star docpad` in your terminal
- [Join our DocPad Community on Gittip!](https://www.gittip.com/for/docpad/)
- Talk about us on Social Media; Twitter, Blogging, Etc
- Write about your experiences of DocPad on your blog
- Do a short less than a minute video testimonial of DocPad on Youtube!
- and just continuing to be awesome



## Skeletons

To add a new skeleton to the skeleton listing:

1. [Add your new skeleton to our `exchange.json` file](https://github.com/bevry/docpad-extras/edit/docpad-6.x/exchange.json)
2. Submit the pull request for it (the page for this should appear automatically once you click "Commit Changes" from the previous link)



## Documentation

To update our documentation:

1. Our documentation is located at the [`docpad/documentation` repository](https://github.com/docpad/documentation)
1. We have [strict documentation criteria](https://github.com/docpad/documentation/blob/master/CONTRIBUTING.md) that all documentation changes must abide by, be sure to read it
1. You can edit a file by opening that file in the repository browser, and then clicking the "Edit" button
1. Once done, click save changes or whatever the button says and this will then take you to a "Submit Pull Request" page
1. Fill in the details and click submit



## Coding Standards
Follow the [Bevry Coding Standards](https://github.com/bevry/community/wiki/Coding-Standards) when writing your changes


## Setup

To get started with developing and contributing code, you must first setup your project for development.

### Setup the DocPad Core for Development

1. Install CoffeeScript globally: `npm install -g coffee-script`
1. Fork the repository of the DocPad Core: https://github.com/bevry/docpad
1. Clone your fork to your machine then cd into it
1. Run `npm install` to install any missing dependencies
1. Run `cake compile` to compile the project (or use `cake watch` to compile everytime a change is made)
1. Run `cake test` to test the project
1. Run `npm link` to make this development instance of the projects available to other projects (via `npm link docpad`)

### Setup a DocPad Plugin for Development

1. Ensure you have DocPad setup for development, by running the DocPad Core instructions above
1. Fork the repository of the DocPad Plugin you wish to edit
1. Clone your fork to your machine then cd into it
1. Run `npm link docpad` to link our local development instance of DocPad that we setup earlier to our DocPad Plugin
1. Run `cake install` to install any missing dependencies
1. Run `cake compile` to compile the project (or use `cake watch` to compile everytime a change is made)
1. Run `cake test` to test the project
1. Run `npm link` to make this development instance of the project available to other projects (via `npm link docpad-plugin-
1. Once you're all good, proceed to filing a pull request of publishing your plugin


## Publishing

### Preparation

1. Make sure your changes are on their own branch that is branched off from master
	1. You can do this by: `git checkout master; git checkout -b your-new-branch`
	1. And push the changes up by: `git push origin your-new-branch`
1. Make sure all tests are passing: `cake test`
	1. If possible, add tests for your change, if you don't know how, mention this in your pull request
1. If the project has a prepublish step, run it: `cake prepublish` (if it doesn't have this step, that command will fail, no worries)

### Testing the DocPad Core against Plugins

Before you submit changes to the DocPad Core you'll want to make sure they don't break any of our officially supported plugins:

1. Clone the [`docpad-extras` repository](https://github.com/bevry/docpad-extras) and cd into it: `cd ~; git clone https://github.com/bevry/docpad-extras.git; cd docpad-extras`
1. Make your development docpad instance available to the plugin runner: `npm link docpad`
1. Install the dependencies: `npm install`
1. Clone the plugins: `./app clone`
1. Test the plugins: `./app test`

### Pull Request

To send your changes for the project owner to merge in:

1. Submit your pull request
	1. When submitting, if the original project has a `dev` or `integrate` branch, use that as the target branch for your pull request instead of the default `master`
	1. By submitting a pull request, you agree that your submission can be used freely and without restraint by those whom your submitting the pull request to

### Publish

To publish your changes as the project owner:

1. Increment the version number in the `package.json` file according to the [semver](http://semver.org/) standard, that is:
	1. If everything will break, increment the major version
	2. If something may break, increment the minor version
	3. If nothing will break, increment the revision version

1. Add an entry to the changelog following the format of the previous entries, an example of this is:
	
	``` markdown
	- v6.29.0 April 1, 2013
		- Progress on [issue #474](https://github.com/bevry/docpad/issues/474)
		- DocPad will now set permissions based on the process's ability
			- Thanks to [Avi Deitcher](https://github.com/deitch), [Stephan Lough](https://github.com/stephanlough) for [issue #165](https://github.com/bevry/docpad/issues/165)
		- Updated dependencies
	```


1. Commit the changes with the title set to something like `v6.29.0. Bugfix. Improvement.` and description set to the changelog entry.
1. Publish the module to npm and create a git tag for it: `cake publish`
1. Push your changes and new tag up to the git repo: `git push origin --all; git push origin --tags`
1. Party!
