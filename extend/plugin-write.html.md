```
title: Write a Plugin
```

## Getting Started

Inside your docpad website directory, create a directory called `plugins`. Inside the `plugins` directory create the directory for your plugin (e.g. `plugins/yourPlugin`), and inside your plugin's directory create these two files:

### plugins/yourPlugin/yourPlugin.plugin.coffee

The simplest version of this file will contain the following:

``` coffee
# Export Plugin
module.exports = (BasePlugin) ->
	# Define Plugin
	class YourPlugin extends BasePlugin
		# Plugin name
		name: 'yourPluginName'
```

What this does is extends our BasePlugin from DocPad, and returns the `YourPlugin` class. Of course you should change the `YourPlugin` references to whatever your plugin is actually called.

The [BasePlugin](https://github.com/bevry/docpad/blob/master/src/lib/plugin.coffee) is important as it provides some of the tucked away magic for our plugins. But what is even more important, is the plugin events that your plugin will hook into to provide it's functionality. [You can discover the plugin events available to you by visiting the Plugin Events wiki page here.](/docpad/events)


### plugins/yourPlugin/package.json

This file should look something like this:

``` json
{
	"name": "docpad-plugin-yourPlugin",
	"version": "2.0.0",
	"description": "DocPad plugin which adds the ability to render Something to Something Else.",
	"homepage": "https://github.com/your-github-username/docpad-plugin-yourPlugin",
	"keywords": [
		"docpad",
		"docpad-plugin",
		"something",
		"somethingElse"
	],
	"author": "Name <email> (url)",
	"maintainers": [
		"Name <email> (url)",
	],
	"contributors": [
		"Name <email> (url)",
	],
	"bugs": {
		"url": "https://github.com/your-github-username/docpad-plugin-yourPlugin/issues"
	},
	"repository" : {
		"type": "git",
		"url": "http://github.com/your-github-username/docpad-plugin-yourPlugin.git"
	},
	"engines" : {
		"node": ">=0.6.0",
		"docpad": "6.x"
	},
	"dependencies": {
		"something": "1.0.x"
	},
	"main": "./yourPlugin.plugin.coffee"
}
```

While it is optional, it is highly recommended - and required if you wish to share your plugin, or if you want DocPad to automatically handle your plugin's dependencies. While DocPad utilizes the [MIT License](http://creativecommons.org/licenses/MIT/), you don't have to.

The reason reason why we do version `2.0.0` is just a general convention. Version 2 plugins are compatible for with DocPad v6, whereas Version 1 plugins are compatible with DocPad v5 (before DocPad v5 plugins were bundled).


## Types of plugins

### Renderers

Renderers are used to convert one particular type of text format, to another type, or rather something to something else.

DocPad will perform these conversions from one format to another by triggering the `render` event. A plugin can hook into this event by adding the `render` function inside it. An example of a something plugin, that renders something to somethingElse would look like this.

``` coffee
# Export Plugin
module.exports = (BasePlugin) ->
	# Define Plugin
	class SomethingPlugin extends BasePlugin

	# ...

	# Render some content
	render: (opts, next) ->
		# Prepare
		{inExtension,outExtension,templateData,file} = opts

		# Check extensions
		if inExtension in ['something'] and outExtension in ['somethingElse']
			# Requires
			something = require('something')

			# Render
			opts.content = something.renderToSomethingElse(opts.content)

		# Done, return back to DocPad
		return next()

	# ...
```

DocPad knows when to call the render event based on the documents extensions. For instance, the document `document.html.md.eco` will have two render events fire. The first render event will contain the `inExtension` as `eco`, and the `outExtension` as `md`. The second render event will contain the `inExtension` as `md`, and the `outExtension` as `html`. This is why generally in our plugins we want to check the values of `inExtension` and `outExtension` to make sure our plugin is performing the correct render.

### Other types

Plugins of other types are generated in the same way as Renderers, they simply aim to achieve different results. While Renderers primarily use the `render` event to trigger their behaviour other plugin types use a variety of events such as `writeBefore` and `parseAfter` to alter the creation of documents and add additional functionality. [Click here for more information on event types](http://bevry.me/docpad/events)

## Reusable plugins

If you are just adding some basic functionality that is specific to a site then everything we've described thus far is probably enough. However if you're doing something thats more generic, or could be useful to other people, then why not create your plugin so its reusable? This has many advantages, you can distribute your plugin on NPM, you can use it across multiple projects, and you can setup unit tests to ensure your plugin works correctly.

First you'll need to setup a directory structure that will contain your plugin, usually this folder becomes a Git repository making it easy to distribute.

Here's an example directory structure for a plugin:

```
docpad-plugin-yourPlugin/
	 src/
		 yourPlugin.plugin.coffee
	 Makefile
	 README.md
	 package.json
```

#### docpad-plugin-yourPlugin/src/yourPlugin.plugin.coffee

`yourPlugin.plugin.coffee` is the same file we created earlier, we've just moved it into its own folder so it can have its own git repository and is easily deployed to NPM. After we've got this plugin setup and installed into NPM then we'll be able to link it back into your site so you can use it during development.

#### docpad-plugin-yourPlugin/package.json

This is the same as previously specified above.

#### docpad-plugin-yourPlugin/Makefile

A makefile makes it a bit easier to compile and test your plugin. This is fairly standard so you probably won't need to modify this file for your plugin.

``` bash
# If you change something here, be sure to reflect the changes in:
# - the scripts section of the package.json file
# - the .travis.yml file

# -----------------
# Variables

BIN=node_modules/.bin/
COFFEE=$(BIN)coffee
OUT=out
SRC=src


# -----------------
# Documentation

# Usage: coffee [options] path/to/script.coffee -- [args]
# -b, --bare		 compile without a top-level function wrapper
# -c, --compile	  compile to JavaScript and save as .js files
# -o, --output	   set the output directory for compiled JavaScript
# -w, --watch		watch scripts for changes and rerun commands


# -----------------
# Commands

# Watch and recompile our files
dev:
	$(COFFEE) -cbwo $(OUT) $(SRC)

# Compile our files
compile:
	$(COFFEE) -cbo $(OUT) $(SRC)

# Clean up
clean:
	rm -Rf $(OUT) node_modules *.log

# Install dependencies
install:
	npm install

# Reset
reset:
	make clean
	make install
	make compile

# Ensure everything is ready for our tests (used by things like travis)
test-prepare:
	make reset
	rm -Rf test/node_modules test/*out test/*.log
	cd test; npm install

# Run our tests
test:
	npm test


# Ensure the listed commands always re-run and are never cached
.PHONY: dev compile clean install reset test-prepare test
```

You should now be able to deploy your plugin on NPM and then install it like any other plugin in DocPad. You can deploy to NPM using the `publish` command, [see here for more details](https://npmjs.org/doc/publish.html). But before you do that don't you want to make sure your plugin works?

## Unit Testing

If you're going to release a plugin for other people to use its probably wise to make sure it works as expected. Thankfully DocPad provides a simple architecture for unit testing plugins. In order to start unit testing we need to add a few files to our folder structure:

```
docpad-plugin-yourPlugin/
	src/
		yourPlugin.plugin.coffee
		yourPlugin.tester.coffee
	test/
		 out-expected/
		 	yourPluginTest.html
		 src/
			 documents/
			 	yourPluginTest.html.eco
		 yourPlugin.test.js
		 package.json
	Makefile
	README.md
	package.json
```

Notice the new `yourPlugin.tester.coffee` and `test` folder. These contain the test runner and the tests themselves.

#### docpad-plugin-yourPlugin/src/yourPlugin.tester.coffee

This file exports a class that will be used to test your plugin. For now there's just the one tester type to extend from, `RendererTester` which by default runs your plugin against a folder of documents and compares the output to the contents of the `out-expected` folder. This is all you'll need for most plugins as we're only really concerned about the input and output of our plugins. For more complex plugins you might want to take a look at the [testers.coffee source](https://github.com/bevry/docpad/blob/master/src/lib/testers.coffee) for more details and other potential testers to extend from.

Below is a simple tester implementation:

``` coffee
# Export Plugin Tester
module.exports = (testers) ->
	# Define Plugin Tester
	class MyTester extends testers.RendererTester
		# Configuration
		docpadConfig:
			logLevel: 5
			enabledPlugins:
				'yourPlugin': true
				'eco': true
```

Note you would need to change `yourPlugin` to whatever you named your plugin in order for this tester to work. Any additional configuration your plugin needs should be added to the `docpadConfig` object here.

#### docpad-plugin-yourPlugin/test/package.json

The `package.json` in the `test` folder should specify all the dependencies for your tests:

``` json
{
	"name": "docpad-plugin-yourPlugin-testsuite",
	"version": "0.1.0",
	"private": true,
	"dependencies": {
		"docpad-plugin-eco": "latest"
	}
}
```

#### docpad-plugin-yourPlugin/test/yourPlugin.test.js

This file simply calls into DocPad and tell it to test our plugin, you will need to modify the `pluginName` property to match your plugin:

```
require('docpad').require('testers').test({pluginPath: __dirname+'/..',pluginName:'yourPlugin'});
```

#### docpad-plugin-yourPlugin/package.json

You'll want to modify the `package.json` for your plugin to support the test process, simply add the `devDependencies` and `scripts` objects to the configuration as shown below:

``` json
{
	// ...
	"devDependencies": {
		"coffee-script": "1.4.x"
	},
	"scripts": {
		"test": "node ./test/yourPlugin.test.js"
	}
	// ...
}
```

These tell NPM how to test the plugin and add the coffee script dependency for development purposes.

### Writing the tests

DocPad's `RendererTester` will setup an instance of DocPad using the configuration specified in your tester above, it will then generate a site using the documents in the `test/src/documents` folder and compare the results with the files in the `test/out-expected` folder. This way you can quickly and easily test how documents in a site are handled by your plugin. For more complex tests you will have to examing the [testers.coffee source](https://github.com/bevry/docpad/blob/master/src/lib/testers.coffee).

### Running the tests

Before we can run our unit tests we'll need to get DocPad and your plugin setup correctly. First you will need to clone a copy of the DocPad repository as you'll need the original source to run the tests. You'll then want to set it up and compile it. We're also going to link this copy of DocPad into your NPM module cache so that whenever you use DocPad it actually points to this copy.

``` bash
git clone https://github.com/bevry/docpad.git
cd docpad
npm install
npm link
cake compile
```

This sets up your copy of DocPad and makes it so that NPM will use this copy instead of the one in the NPM repository. Next you'll need to do a similar setup for your plugin.

``` bash
cd docpad-plugin-yourPlugin
npm install
npm link docpad
cake compile
```

This will install all the dependencies for your plugin, and link the DocPad instance in your plugin with the one we just cloned from GitHub.

Now we're ready to run the tests!

``` bash
cake test
```

Hopefully you should now see output similar to the following:

``` bash
> docpad-plugin-yourPlugin@0.1.4 test c:\Workspace\docpad-plugin-yourPlugin
> node ./test/yourPlugin.test.js

joe
joe > yourPlugin
joe > yourPlugin > create
joe > yourPlugin > create OK
joe > yourPlugin > load plugin yourPlugin
joe > yourPlugin > load plugin yourPlugin OK
joe > yourPlugin > generate
joe > yourPlugin > generate > action
joe > yourPlugin > generate > action OK
joe > yourPlugin > generate > results
joe > yourPlugin > generate > results OK
joe > yourPlugin > generate OK
joe > yourPlugin > server
joe > yourPlugin > server OK
joe > yourPlugin > finish up
joe > yourPlugin > finish up OK
joe > yourPlugin OK
joe OK

6/6 tests ran successfully, everything passed
```

Writing good unit tests is hard, but just try to cover all the possible inputs and expected outputs for your plugin and you will be making a good start.
