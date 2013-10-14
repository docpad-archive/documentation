```
title: Write a Plugin
```


## Getting Started

Inside your docpad website directory, create a directory called `plugins`. Inside the `plugins` directory create the directory for your plugin (e.g. `plugins/yourpluginname`), and inside your plugin's directory create these two files:


### `src/yourpluginname.plugin.coffee`

The simplest version of this file will contain the following:

``` coffee
# Export Plugin
module.exports = (BasePlugin) ->
	# Define Plugin
	class YourpluginnamePlugin extends BasePlugin
		# Plugin name
		name: 'yourpluginname'
```

What this does is extends our BasePlugin from DocPad, and returns the `YourPlugin` class. Of course you should change the `YourPlugin` references to whatever your plugin is actually called.

The [BasePlugin](https://github.com/bevry/docpad/blob/master/src/lib/plugin.coffee) is important as it provides some of the tucked away magic for our plugins. But what is even more important, is the plugin events that your plugin will hook into to provide it's functionality. [You can discover the plugin events available to you on the Events Page.](/docpad/events)


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
		"node": ">=0.8"
	},
	"peerDependencies": {
	"main": "./src/yourpluginname.plugin.coffee"
}
```

The reason reason why we do version `2.0.0` is just a general convention. Version 2 plugins are compatible for with DocPad v6, whereas Version 1 plugins are compatible with DocPad v5 (before DocPad v5 plugins were bundled).



## Types of plugins

### Renderers

Renderers are used to convert one particular type of text format, to another type, or rather something to something else.

DocPad will perform these conversions from one format to another by triggering the `render` event. A plugin can hook into this event by adding the `render` function inside it.

- [Here is the plugin file of an example plugin that performs the synchronous conversion of transorming the content of `txt` files that have the extra `uc` or `uppercase` extension to upper case.](/plugin/yourpluginname/blob/master/src/yourpluginname.plugin.coffee)
- [Here is the plugin file of the coffeekup plugin that accepts configuration and performs and asynchronous conversion.](/plugin/coffeekup/blob/master/src/coffeekup.plugin.coffee)

An important thing to note about the rendering process is that DocPad knows when and how to call the render event based on the documents extensions. For instance, the document `document.html.md.eco` will have two render events fire. The first render event will contain the `inExtension` as `eco`, and the `outExtension` as `md`. The second render event will contain the `inExtension` as `md`, and the `outExtension` as `html`. This is why generally in our plugins we want to check the values of `inExtension` and `outExtension` to make sure our plugin is performing the correct render.


### Other types

Plugins of other types are generated in the same way as Renderers, they simply aim to achieve different results. While Renderers primarily use the `render` event to trigger their behaviour other plugin types use a variety of events such as `writeBefore` and `parseAfter` to alter the creation of documents and add additional functionality. [Click here for more information on event types](/docpad/events)




## Reusable plugins

If you are just adding some basic functionality that is specific to a site then everything we've described thus far is probably enough. However if you're doing something thats more generic, or could be useful to other people, then why not create your plugin so its reusable? This has many advantages, you can distribute your plugin on NPM, you can use it across multiple projects, and you can setup unit tests to ensure your plugin works correctly.

Here's the extra files that we will need to add to our plugin:

```
.gitignore
.npmignore
Cakefile
LICENSE.md
README.md
```

You can find the contents of these files on our [example plugin repository](/plugin/yourpluginname).

The `Cakefile` however is worth mentioning, as it makes it to compile our plugin (`cake compile` to compile once, `cake dev` to compile on change) so we don't have to compile it at run-time each time. If you decide to use the cake file to pre-compile our plugin, you'll want to update your `main` property in your plugin's `package.json` to point to the compiled file like so:

``` javascript
{
	// ...
	"main": "./out/yourpluginname.plugin.js"
	// ...
}
```



## Adding tests

We can also add tests for our plugin to ensure it is working correctly. DocPad makes this process pretty darn easy. To do so, we'll need to add these extra files:


Here's the extra files that we will need to add to our plugin:

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

This file simply calls into DocPad and tell it to test our plugin, you will need to modify the `pluginName` property to match your plugin:

```
# Test our plugin using DocPad's Testers
require('docpad').require('testers').test({pluginPath: __dirname+'/..'})
```


#### `src/yourpluginname.tester.coffee`

This file is optional but is essential if you want to tell DocPad to load additional plugins as well as yours, or if you need to do advanced configuration of the test environment. The file exports a class that will be used to test your plugin. For now there's just the one tester type to extend from, `RendererTester` which by default runs your plugin against a folder of documents and compares the output to the contents of the `out-expected` folder. This is all you'll need for most plugins as we're only really concerned about the input and output of our plugins.

The [Text Plugin](h/plugin/text) is a great example of this, you can find its [tester file here](/plugin/text/blob/master/src/text.tester.coffee).

For more complex plugins you might want to take a look at the [testers.coffee source](https://github.com/bevry/docpad/blob/master/src/lib/testers.coffee) for more details and other potential testers to extend from.


#### `test/package.json`

This file is optional but is essential if you want your test site required other plugins than just your one.

The [Text Plugin](/plugin/text) is a great example of this, you can find its [test site's package.json file here](/plugin/text/blob/master/test/package.json).


#### `package.json`

You'll want to modify the `package.json` for your plugin to support the test process, simply add the `devDependencies` and `scripts` objects to the configuration as shown below:

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
cd docpad-plugin-yourpluginname
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

Writing good unit tests is hard, but just try to cover all the possible inputs and expected outputs for your plugin and you will be making a good start.
