## Getting Started

*This guide applies to version 3 of DocPad. [If you are looking for the version 1 & 2 guide, click here.](https://github.com/bevry/docpad/wiki/Extending-v1&2)*

Inside your docpad website directory, create a plugins directory. Inside it, create a new file called `something.plugin.coffee` and let it contain the following:

	# Export Plugin
	module.exports = (BasePlugin) ->
		# Define Plugin
		class SomethingPlugin extends BasePlugin
			# Plugin name
			name: 'something'

What this does is receives our BasePlugin from DocPad, and returns our `SomethingPlugin` class. You should rename the somethings into whatever you plugin is actually called. The BasePlugin is important as it provides all the tucked away magic for our plugins.

It's also a good idea to take a look at what's inside the [base plugin](https://github.com/bevry/docpad/blob/master/lib/base-plugin.coffee) to discover what events are available to you.

## Writing a renderer

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

DocPad knows when to call the render event based on the documents extensions. For instance, the document `document.html.md.eco` will have two render events fire. The first render event will contain the `inExtension` as `eco`, and the `outExtension` as `md`. The second render event will contain the `inExtension` as `md`, and the `outExtension` as `eco`. This is why generally in our plugins we want to check the values of `inExtension` and `outExtension` to make sure our plugin is performing the correct render.

### Existing Plugins

[You can take a look at the existing bundled plugins inside DocPad here](https://github.com/bevry/docpad/blob/master/lib/exchange) - they will give you a good foundation on how to go about your own. [You can also discover a showcase of all available plugins by clicking here.](https://github.com/bevry/docpad/wiki/Extensions)

### Coding Standards

While you are free to write your plugins in whichever standards you wish, [you can find the coding standards which the DocPad core uses here.](https://github.com/bevry/external/wiki/Coding-Standards)