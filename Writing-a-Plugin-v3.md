## Version Note

**This guide applies to version 3 of DocPad.** [The latest version guide is here](https://github.com/bevry/docpad/wiki/Writing-a-Plugin).

## Getting Started

Inside your docpad website directory, create a directory called `plugins`. Inside the `plugins` directory create the directory for your plugin (e.g. `plugins/yourPlugin`), and inside your plugin's directory create these two files:

### plugins/yourPlugin/yourPlugin.plugin.coffee

The most simplest version of this file will contain the following:

	# Export Plugin
	module.exports = (BasePlugin) ->
		# Define Plugin
		class YourPlugin extends BasePlugin
			# Plugin name
			name: 'yourPluginName'

What this does is receives our BasePlugin from DocPad, and returns the `YourPlugin` class. Of course you should change the your plugin references to whatever your plugin is actually called.

The [BasePlugin](https://github.com/bevry/docpad/blob/master/lib/base-plugin.coffee) is important as it provides some of the tucked away magic for out plugins. But what is event more important, is the plugin events that your plugin will hook into to provide it's functionality. [You can discover the plugin events available to you by visiting the Plugin Events wiki page here.](https://github.com/bevry/docpad/wiki/Plugin-Events)


### plugins/yourPlugin/package.json

This file should look something like this:

	{
		"name": "docpad-yourPlugin",
		"version": "0.1.0",
		"description": "DocPad plugin which adds the ability to render Something to Something Else.",
		"homepage": "https://github.com/your-github-username/docpad-yourPlugin",
		"keywords": [
			"docpad",
			"docpad-plugin",
			"something",
			"somethingElse"
		],
		"author": {
			"name": "Your firstname and lastname go here",
			"email": "your@email.address",
			"url": "http://your.website"
		},
		"maintainers": [
			{
				"name": "Your firstname and lastname go here",
				"email": "your@email.address",
				"url": "http://your.website"
			}
		],
		"contributors": [
			{
				"name": "Your firstname and lastname go here",
				"email": "your@email.address",
				"url": "http://your.website"
			}
		],
		"bugs": {
			"url": "https://github.com/your-github-username/docpad-yourPlugin/issues"
		},
		"licenses": [
			{
				"type": "MIT",
				"url": "http://creativecommons.org/licenses/MIT/"
			}
		],
		"repository" : {
			"type": "git",
			"url": "http://github.com/your-github-username/docpad-yourPlugin.git"
		},
		"dependencies": {
			"something": "1.0.x"
		},
		"engines" : {
			"node": ">=0.4.0"
		},
		"main": "./something.plugin.coffee"
	}

While it is optional, it is highly recommended - and required if you wish to share your plugin, or if you want DocPad to automatically handle your plugin's dependencies. While DocPad utilizes the [MIT License](http://creativecommons.org/licenses/MIT/), you don't have to.


## Types of plugins

### Renderers

Renderers are used to convert one particular type of text format, to another type, or rather something to something else. A concrete example of this is the [bundled markdown plugin](https://github.com/bevry/docpad/blob/master/lib/exchange/plugins/markdown/markdown.plugin.coffee), which renders [Markdown](http://daringfireball.net/projects/markdown/basics) to HTML.

DocPad will perform these conversions from one format to another by triggering the `render` event. A plugin can hook into this event by adding the `render` function inside it. An example of a something plugin, that renders something to somethingElse would look like this.

	# Export Plugin
	module.exports = (BasePlugin) ->
		# Define Plugin
		class SomethingPlugin extends BasePlugin
		
		# ...
	
		# Render some content
		render: ({inExtension,outExtension,templateData,file}, next) ->
			# Check extensions
			if inExtension in ['something'] and outExtension in ['somethingElse']
				# Requires
				something = require('something')

				# Render
				file.content = something.renderToSomethingElse(file.content)
		
			# Done, return back to DocPad
			return next()
	
		# ...

DocPad knows when to call the render event based on the documents extensions. For instance, the document `document.html.md.eco` will have two render events fire. The first render event will contain the `inExtension` as `eco`, and the `outExtension` as `md`. The second render event will contain the `inExtension` as `md`, and the `outExtension` as `html`. This is why generally in our plugins we want to check the values of `inExtension` and `outExtension` to make sure our plugin is performing the correct render.


### Other types

Documentation about other types is soon to come.

