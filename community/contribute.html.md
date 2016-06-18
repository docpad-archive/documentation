```
title: Contributing
```


## Bevry

For the most part, DocPad inherits from the [Bevry Community's Contribution Guide](https://learn.bevry.me/community/contribute), with the following exceptions.


## Skeletons

To add a new skeleton to the skeleton listing:

1. Add your new skeleton to our [`exchange.json` file](https://github.com/docpad/extras/edit/docpad-6.x/exchange.json)
1. Submit the pull request for it (the page for this should appear automatically once you click "Commit Changes" from the previous link)



## Setup

To get started with developing and contributing code, you must first setup your project for development.


### Setup the DocPad core for development

To setup a development environment for contributing to the DocPad core follow these steps:

1. Fork the repository of the DocPad Core: https://github.com/docpad/docpad
1. Clone your fork to your machine then `cd` into it
1. Run `npm run prepare` to install any missing dependencies
1. Run `npm run compile` to compile the project
1. Run `npm test` to test the project
1. Run `npm link` to make this development instance of the projects available to other projects (via `npm link docpad`)


### Setup a DocPad plugin for development

To setup a development environment for contributing to a plugin follow these steps:

1. Ensure you have DocPad setup for development, by running the DocPad core instructions above
1. Fork the repository of the DocPad plugin you wish to edit
1. Clone your fork to your machine then `cd` into it
1. Run `npm link docpad` to link our local development instance of DocPad that we setup earlier to our DocPad plugin
1. Run `cake install` to install any missing dependencies
1. Run `cake compile` to compile the project
1. Run `cake test` to test the project
1. Run `npm link` to make this development instance of the project available to other projects (via `npm link docpad-plugin-PLUGINNAME`)



### Testing the DocPad core against plugins

Before you submit changes to the DocPad core you'll want to make sure they don't break any of our officially supported plugins:

1. Clone the [`docpad/extras` repository](https://github.com/docpad/extras) and `cd` into it
1. Checkout the `docpad-6.x` branch: `git checkout docpad-6.x`
1. Make your development DocPad instance available to the plugin runner (run `npm link docpad`)
1. Install the dependencies: `npm install`
1. Clone the plugins: `./app clone`
1. Test the plugins: `./app test`
