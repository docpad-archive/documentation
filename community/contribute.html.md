```
title: Contributing
```


## Support

To get support:

- For bug reports relating to the core, use our [GitHub Issue Tracker](https://github.com/bevry/docpad/issues)
- For bug reports relating to plugins, use their GitHub Issue Tracker
  - You can find the link by going to the plugin's page, then looking for the "Issues" button
- With your bug reports, be sure to specify:
		- Your docpad version `docpad --version`
		- Your node version `node --version`
		- Your npm version `npm --version`
		- Your operating system's name, architecture, and version
		- What you did
		- What happened
		- What you expected
- For everything else that isn't bug reports (e.g. questions, support, etc), use our [Official Support Channels](http://docpad.org/support)



## Skeletons

To add a new skeleton to the skeleton listing:

1. Add your new skeleton to this JSON file: https://github.com/bevry/docpad-extras/blob/docpad-6.x/exchange.json
2. Submit the pull request for it (the page for this should appear automatically when you click "Commit Changes")



## Documentation

To update our documentation:

1. Our documentation for DocPad is stored in this repository: https://github.com/bevry/docpad-documentation
2. Documentation is written in Markdown
3. You can edit a file by opening that file in the repository browser, and then clicking the "Edit" button
4. Once done, click save changes or whatever the button says and this will then take you to a "Submit Pull Request" page
5. Fill in the details and click submit



## Development

To get started making changes to the DocPad core:

1. Fork the DocPad Repository
1. Clone your fork and cd into it
1. Ensure CoffeeScript is installed globally; `npm install -g coffee-script`
1. Run `cake setup` to setup our project for development
1. Run `npm link` to link our local copy as the global instance (so it is available via `docpad`)
1. Run `cake dev` to compile our source files and recompile on changes



## Pull Requests

To get some changes you've made into the official repository:

1. Make your change sin their own branch that is branched off from master, e.g. `git checkout master; git checkout -b your-new-branch`
1. Test your changes before you submit the pull request (see testing section), if possible, add tests for your change - if you don't know how to fix the tests, submit your pull request and say so, happy to help (but it will slow down integration)
1. **When submitting the pull request, specify the `dev` branch as the integration branch (the integration branch is which branch your pull request will be merged into on the official repo)**
1. If you'd like, feel free to add yourself to the contributors section of the `package.json` file if it exists
1. By submitting a pull request, you agree that your submission can be used freely and without restraint by those whom your submitting the pull request to



## Testing

Before you submit your changes you'll want to make sure your changes still work with our test suite. You can do this by:

1. Run `npm test` to run the docpad tests
	1. There are several types of tests that run, the most common is the rendering test, which compares files inside `test/out` to `test/out-expected`
1. Sometimes you'll also want to test your changes against our supported plugins, to do this:
	1. Clone our the [docpad-extras](https://github.com/bevry/docpad-extras) repository and cd into it: `git clone https://github.com/bevry/docpad-extras.git; cd docpad-extras`
	1. Install the dependencies: `npm install`
	1. Make your docpad setup available: `npm link docpad`
	1. Clone out the plugins: `cake clone`
	1. Test the plugins: `cake test`



## Publishing

To publish a new version:

1. Pull in the latest changes from the master and dev branches
1. Make sure the tests work, if your publishing a new docpad verison also make sure the [docpad-extras](https://github.com/bevry/docpad-extras) tests work
1. Add an entry to the changelog following the format of the previous entries, an example of this is:
	
	``` markdown
	- v6.29.0 April 1, 2013
		- Progress on [issue #474](https://github.com/bevry/docpad/issues/474)
		- DocPad will now set permissions based on the process's ability
			- Thanks to [Avi Deitcher](https://github.com/deitch), [Stephan Lough](https://github.com/stephanlough) for [issue #165](https://github.com/bevry/docpad/issues/165)
		- Updated dependencies
	```

1. Add any new contributors to the `package.json` file, for their URL use their github profile URL
1. Increment the version number in the `package.json` file according to the [semver](http://semver.org/) standard, that is:
	1. If everything will break, increment the major version
	2. If somethings will break, increment the minor version
	3. If nothing will break, increment the revision version
1. Commit the changes with the title set to something like `v6.29.0. Bugfix. Improvement.` and description set to the changelog entry.
1. Tag the commit as the version number, e.g. `git tag v6.29.0`
1. Publish the module: `npm publish`
1. Merge your changes into the master and dev branches
1. Push your changes and new tag up to the git repo: `git push origin --all; git push origin --tags`
1. Party!
