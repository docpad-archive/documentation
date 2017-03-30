```
title: Write a Plugin
```


## Getting Started

1. Inside your DocPad website directory, create a directory called `plugins` (i.e. `yourwebsite/plugins`)

1. Inside your new plugins directory, create the directory for your plugin (i.e. `yourwebsite/plugins/yourpluginname`)

1. Inside your new plugin directory, run the following commands to clone out the [example plugin](https://github.com/docpad/docpad-plugin-yourpluginname) that we will use as our base:

	```
	git init
	git remote add base https://github.com/docpad/docpad-plugin-yourpluginname.git
	git pull base master
	npm run our:setup     # installs dependencies, and prepares the docpad dependency for development
	npm run our:commpile  # compile your plugin
	```

You will now find several files.

An important thing to note about the `package.json` file is that our plugin starts with the version `2.0.0`. This is because v2 plugins are compatible for with DocPad v6, whereas v1 plugins are compatible with DocPad v5. [This is currently a necessary convention that you must follow.](https://github.com/docpad/docpad/issues/691)

The `src/yourpluginname.plugin.coffee` file is the logic for our plugin. It's current contents will uppercase all documents with `.uc` or `.uppercase` extension. The simplest form of this file (which wouldn't perform anything) would be:

``` coffee
# Export Plugin
module.exports = (BasePlugin) ->
	# Define Plugin
	class YourpluginnamePlugin extends BasePlugin
		# Plugin name
		name: 'yourpluginname'
```

A more verbose form of this would be:

``` coffee
# Export a function that will accept the BasePlugin class from DocPad and then will return our own class that will extend it.
module.exports = (BasePlugin) ->
	# Create and return our own class that extends the BasePlugin class
	class YourpluginnamePlugin extends BasePlugin
		# Define our plugin name
		name: 'yourpluginname'

		# The rest of your plugin definition goes here
		# ...
```

Extending the [BasePlugin](https://github.com/docpad/docpad/blob/master/src/lib/plugin.coffee) class is important as it provides some of the tucked away magic for our plugins, such as automatically listening for events when a plugin method of the event name is defined. [You can discover the plugin events available to you on the Events Page.](https://docpad.org/docs/events)

If you prefer to write your plugins with ES6 JavaScript, you can do it like so:

``` javascript
// Export Plugin
module.exports = function (BasePlugin) {
	// Define Plugin
	return class YourpluginnamePlugin extends ({
		// Plugin name
		get name () { return 'yourpluginname' }
		
		// Initial plugin configuration
		get initialConfig () { return {} }
	});
};
```

If you prefer to write your plugins with ES5 JavaScript, you can use the `BasePlugin.extend({})` method like so:

``` javascript
// Export Plugin
module.exports = function (BasePlugin) {
	// Define Plugin
	return BasePlugin.extend({
		// Plugin name
		name: 'yourpluginname'
	});
};
```


## Types of plugins

### Renderers

Renderers are used to convert one particular type of text format, to another type, or rather something to something else.

DocPad will perform these conversions from one format to another by triggering the `render` event. A plugin can hook into this event by adding the `render` function inside it.

- [Here is the plugin file of an example plugin that performs the synchronous conversion of transforming the content of `txt` files that have the extra `uc` or `uppercase` extension to upper case.](https://github.com/docpad/docpad-plugin-yourpluginname/blob/master/src/yourpluginname.plugin.coffee)
- [Here is the plugin file of the coffeekup plugin that accepts configuration and performs and asynchronous conversion.](https://github.com/docpad/docpad-plugin-coffeekup/blob/master/src/coffeekup.plugin.coffee)

An important thing to note about the rendering process is that DocPad knows when and how to call the render event based on the documents extensions. For instance, the document `document.html.md.eco` will have two render events fire. The first render event will contain the `inExtension` as `eco`, and the `outExtension` as `md`. The second render event will contain the `inExtension` as `md`, and the `outExtension` as `html`. This is why generally in our plugins we want to check the values of `inExtension` and `outExtension` to make sure our plugin is performing the correct render.


### Other types

Plugins of other types are generated in the same way as Renderers, they simply aim to achieve different results. While Renderers primarily use the `render` event to trigger their behaviour other plugin types use a variety of events such as `writeBefore` and `parseAfter` to alter the creation of documents and add additional functionality. [Click here for more information on event types](https://docpad.org/docs/events)



## Making your Plugin Yours

Probably the first thing you want to do is to change the name and description of your plugin. There are several spots you would want to do this:

- The filenames in `src`

- The classname and plugin name in `src/yourpluginname.plugin.coffee`

- Various properties inside `package.json`

- The heading and description inside `README.md`

Once you update your `package.json` file with the new values, you would want to run `npm run our:release:prepare` which will also compile your plugin's meta files with [projectz](https://github.com/bevry/projectz), which is very useful for automatically updating your `README.md` and `LICENSE.md` files with the latest details for your `package.json` file.


## Testing your Plugin

For testing our plugins, we will take note of the following files:

```
src/
	pluginname.test.coffee
	pluginname.tester.coffee
test/
	out-expected/
		...
	src/
		render/
			...
	package.json (optional)
```


#### `src/yourpluginname.test.coffee`

The compiled version of this file is what our test running executes (`package.json:scripts:test`). It simply loads DocPad's test helpers to test our plugin.

Optionally you can use this file to run your tests multiple times but in different environments. For example, the [paged plugin's customisations](https://github.com/docpad/docpad-plugin-paged/blob/master/src/paged.test.coffee) allows it to test its compatibility with other DocPad plugins.

``` coffeescript
# Test our plugin using DocPad's Testers
require('docpad').require('testers').test({testerClass: 'RendererTester', pluginPath: __dirname+'/..'})
```


#### `src/yourpluginname.tester.coffee`

This file is optional but is essential if you want to tell DocPad to load additional plugins as well as yours, or if you need to do advanced configuration of the test environment. The file exports a class that will be used to test your plugin. For now there's just the one tester type to extend from, `RendererTester` which by default runs your plugin against a folder of documents and compares the output to the contents of the `out-expected` folder. This is all you'll need for most plugins as we're only really concerned about the input and output of our plugins.

The [Eco Plugin](https://github.com/docpad/docpad-plugin-eco) is a great example of this, you can find its [tester file here](https://github.com/docpad/docpad-plugin-eco/blob/master/src/eco.tester.coffee).

For more complex plugins you might want to take a look at the [testers.coffee source](https://github.com/docpad/docpad/blob/master/src/lib/testers.coffee) for more details and other potential testers to extend from.


#### `test/package.json`

This file is optional but is essential if you want your test site require other plugins than just your one.

The [Text Plugin](https://github.com/docpad/docpad-plugin-text) is a great example of this, you can find its [test site's package.json file here](https://github.com/docpad/docpad-plugin-text/blob/master/test/package.json).



### Writing the tests

DocPad's `RendererTester` will setup an instance of DocPad using the configuration specified in your tester above, it will then generate a site using the documents in the `test/src/render` folder and compare the results with the files in the `test/out-expected` folder. This way you can quickly and easily test how documents in a site are handled by your plugin. For more complex tests you will have to examing the [testers.coffee source](https://github.com/docpad/docpad/blob/master/src/lib/testers.coffee).


### Running the tests

To run the full test suite, including compilation and meta updates, you would run:

``` bash
npm run our:release:prepare
```

Which will output something like:

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


### Linking DocPad

If you are working on a development copy of DocPad, you can use it instead by running the following inside the DocPad instance directory:

```
npm run our:release:prepare
npm link
```

Then inside your plugin, run:

```
npm link docpad
npm run our:release:prepare
```


## Maintenance

If your plugin becomes popular with the DocPad community, you will have the option of making it an official plugin. This means:

1. Transferring it to the DocPad GitHub Organisation so that it can be maintained by the DocPad Extras Team
1. Running `npm owner add bevryme` in your plugin directory to give the DocPad Core Team publishing rights
1. The Core Team can then give publish rights to whomever from the Extra Team wants to take accountability for the plugin
1. The Extras Team can then alert the maintainers of the plugin of things that need doing (preferably via a pull request) so the maintainers can just merge and publish
