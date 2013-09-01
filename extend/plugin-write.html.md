```
title: Write a Plugin
```


## Getting Started

In your DocPad project’s directory, create a directory called `plugins`. In `plugins`, create the directory for your plugin (e.g. `plugins/yourpluginname`). 

Inside your plugin’s directory, create these two files:

- `yourpluginname.plugin.coffee`
- `package.json`

More about these files follows.


### `yourpluginname.plugin.coffee`

The simplest version of this file will contain the following:

``` coffee
# Export Plugin
module.exports = (BasePlugin) ->
	# Define Plugin
	class YourpluginnamePlugin extends BasePlugin
		# Plugin name
		name: 'yourpluginname'
```

This extends the `BasePlugin` class (provided by DocPad), and returns the `YourPlugin` class. (You probably want to come up with a better name, though. ☺)

The [`BasePlugin`](https://github.com/bevry/docpad/blob/master/src/lib/plugin.coffee) is important. Among other kinds of magic it provides for plugins, it lets your plugin to hook into the events it needs to, in order to provide its functionality. [You can discover the plugin events available to you on the Events Page.](/docpad/events)  


### `package.json`

This file should look something like this:

``` json
{
	"name": "docpad-plugin-yourpluginname",
	"version": "2.0.0",
	"description": "DocPad plugin that adds the ability to render Something to Something Else",
	"homepage": "https://github.com/yourgithubusername/docpad-plugin-yourpluginname",
	"keywords": [
		"docpad",
		"docpad-plugin",
		"something",
		"somethingelse"
	],
	"author": "Copyright holders name <copyright holder's email> (copyright holder's website url)",
	"maintainers": [
		"Your name <your email> (your github url)"
	],
	"contributors": [
		"Your name <your email> (your github url)"
	],
	"bugs": {
		"url": "https://github.com/yourgithubusername/docpad-plugin-yourpluginname/issues"
	},
	"repository" : {
		"type": "git",
		"url": "https://github.com/yourgithubusername/docpad-plugin-yourpluginname.git"
	},
	"engines" : {
		"node": ">=0.8",
		"docpad": ">=6"
	},
	"main": "./src/yourpluginname.plugin.coffee"
}
```

The reason for using version `2.0.0` is just a convention. Version 2 plugins are compatible with DocPad v6, whereas Version 1 plugins are compatible with DocPad v5. (Before DocPad v5, plugins were bundled).



## Types of plugins

### Renderers

Renderers are used to convert one particular type of text format into another.

DocPad performs these conversions by firing the `render` event. Plugins can hook into this event by adding the `render` function inside it.

- [Here’s an example plugin that performs a synchronous conversion of transforming the contents of `*.txt.uc` files to upper case.](/plugin/yourpluginname/blob/master/src/yourpluginname.plugin.coffee)
- [Here’s the **coffeekup** plugin, which accepts configuration and performs an asynchronous conversion.](/plugin/coffeekup/blob/master/src/coffeekup.plugin.coffee)

**Important note:** DocPad knows when and how to call the `render` event based on documents’ extensions. For instance, the document `document.html.md.t` will fire two `render` events: 

1. The first render event will contain the `inExtension` as `eco`, and the `outExtension` as `md`
2. The second render event will contain the `inExtension` as `md`, and the `outExtension` as `html`. 

This is why, in general, plugins should check the values of `inExtension` and `outExtension`, to be certain they are performing the correct render.


### Other types

Plugins of other types are generated in the same way as Renderers. They simply aim to achieve different results. While Renderers primarily use the `render` event to trigger their behaviour, other types of plugins use a variety of events (such as `writeBefore` and `parseAfter`) to alter the creation of documents, and add additional functionality. [Click here for more information on event types](/docpad/events).




## Reusable plugins

If you’re just adding some basic, site-specific functionality, then everything described thus far is probably enough. 

However, if you’re doing something more generic, or might be useful to others, why not make your plugin reusable? This has many advantages: you can distribute your plugin on NPM, use it across multiple projects, and write unit tests to ensure your plugin works correctly.

Here are the extra files you’ll need to make a reusable plugin:

```
.gitignore
.npmignore
Cakefile
LICENSE.md
README.md
```

You can find the contents of these files on our [example plugin repository](/plugin/yourpluginname).

The `Cakefile` is special. On the command line, run `cake compile` to compile your plugin once, or `cake dev` to compile our plugin whenever it changes. 

If you use the `Cakefile` to pre-compile your plugin, you’ll need to update the `main` property (in your plugin’s `package.json`), so it points to the compiled file:

``` javascript
{
	// ...
	"main": "./out/yourpluginname.plugin.js"
	// ...
}
```



## Adding tests

You can add tests for your plugin to ensure it’s works correctly. DocPad makes this pretty darn easy. 

To do so, you’ll need to add these extra files:

```
src/
	pluginname.test.coffee
	pluginname.tester.coffee (optional)
test/
	out-expected/
		...
	src/
		documents/
			...
	package.json (optional)
```

#### `src/yourpluginname.test.coffee`

This file simply calls DocPad and tells it to test your plugin. You’ll need to modify the `pluginName` property to match your plugin:

```
# Test our plugin using DocPad's Testers
require('docpad').require('testers').test({pluginPath: __dirname+'/..'})
```


#### `src/yourpluginname.tester.coffee`

This file is essential if your plugin wants DocPad to load additional plugins, or if you need to do advanced configuration of the test environment. 

The file exports a class that will be used to test your plugin. For now, there’s only one tester type to extend from: `RendererTester`. By default, it runs your plugin against a folder of documents, and compares the output to the contents of the `out-expected` folder. 

That’s all you'll need for most plugins. Usually, a plugin’s only real concern is about its input and output.

The [Text Plugin](h/plugin/text) is a great example of this. You can find its [tester file here](/plugin/text/blob/master/src/text.tester.coffee).

For more complex plugins, you might want to look at the [testers.coffee source](https://github.com/bevry/docpad/blob/master/src/lib/testers.coffee) for details (and other potential testers to extend from).


#### `test/package.json`

This file is essential if you want your test site to require other plugins (besides yours).

The [Text Plugin](/plugin/text) is a great example of this. You can find its [`package.json` file here](/plugin/text/blob/master/test/package.json).


#### `package.json`

You’ll want to modify your plugin’s `package.json` to support the test process. Simply add `devDependencies` and `scripts` objects to the configuration:

``` javascript
{
	// ...
	"devDependencies": {
		"coffee-script": "~1.6.2"
	},
	"scripts": {
		"test": "node ./test/yourpluginname.test.js"
	}
	// ...
}
```

These tell NPM how to test the plugin, and add the `coffee-script` dependency for development purposes.


### Writing the tests

DocPad’s `RendererTester` sets up a DocPad instance using your tester’s configuration. Then it generates a site using the documents in `test/src/documents/`, and compares the results with the files in `test/out-expected/`. With this you can quickly and easily test how documents are handled by your plugin. 

For more complex tests, you will have to examine the [`testers.coffee` source](https://github.com/bevry/docpad/blob/master/src/lib/testers.coffee).


### Running the tests

Before you can run your unit tests, you’ll need to get DocPad and your plugin setup correctly. 

First, you’ll need to clone the DocPad repository, since you’ll need the original source to run the tests. Then you should set it up and compile it. You’re also going to link this copy of DocPad into your NPM module’s cache (so that whenever you use DocPad, it actually points to this copy):

``` bash
git clone https://github.com/bevry/docpad.git
cd docpad
npm install
npm link
cake compile
```

This sets up a copy of DocPad tells NPM to use this copy instead of the one in the NPM repository. 

Next, you’ll need to do a similar procedure for your plugin:

``` bash
cd docpad-plugin-yourpluginname
npm install
npm link docpad
cake compile
```

This installs all of your plugin’s dependencies, and links the DocPad instance in your plugin with the one you just cloned from GitHub.

Now you’re ready to run the tests!

``` bash
cake test
```

If everything is working as it should, you should see something similar to this:

``` bash
> docpad-plugin-yourpluginname@2.0.0 test /Users/balupton/Projects/docpad-extras/plugins/yourpluginname
> node ./out/yourpluginname.test.js

yourpluginname
yourpluginname ➞  create
yourpluginname ➞  create ✔   
yourpluginname ➞  load plugin yourpluginname
yourpluginname ➞  load plugin yourpluginname ✔   
yourpluginname ➞  generate
yourpluginname ➞  generate ➞  action
yourpluginname ➞  generate ➞  action ✔   
yourpluginname ➞  generate ➞  results
yourpluginname ➞  generate ➞  results ✔   
yourpluginname ➞  generate ✔  
yourpluginname ➞  server
yourpluginname ➞  server ✔   
yourpluginname ➞  finish up
yourpluginname ➞  finish up ✔   
yourpluginname ✔  

6/6 tests ran successfully, everything passed
OK
```

Writing good unit tests is hard. Just try to cover all the possible inputs and expected outputs for your plugin, and you’ll be off to a good start.
