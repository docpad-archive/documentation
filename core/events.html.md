## Using Events

### Event Handler Structure

Event handlers in DocPad receive two arguments, both of which are optional: 

1. `opts` which is an object filled with properties that the event may provide to you. 
2. `next` which is a completion callback. 

Events are fired in a synchronous (serial) fashion. That means that events are handled in the order they are fired.

Omitting the `next` callback is perfectly valid and encouraged in synchronous code. Synchronous code runs by starting a task, completing it, and then moving onto the next one. Asynchronous, by contrast, starts tasks that may complete in *any* order.  When an asynchronous task completes, it runs a callback function (`next`) to notify the rest of the program that it’s done.


### Inside your Configuration File

You can bind to events inside your DocPad configuration file by adding them to the `events` property. 

In a `docpad.coffee` config file, here’s how you’d bind to the `serverExtend` event:

``` coffeescript
docpadConfig =

	# =================================
	# DocPad Events

	# Here we can define handlers for events that DocPad fires
	# You can find a full listing of events on the DocPad Wiki
	events:

		# Server Extend
		# Used to add our own custom routes to the server before the docpad routes are added
		serverExtend: (opts) ->
			# Extract the server from the options
			{server} = opts
			docpad = @docpad

			# Perform our server extensions
			# ...

# Export our DocPad Configuration
module.exports = docpadConfig
```

The context (what `this`/`@` points to) of event handlers is a shared object between the event handlers that contains only the DocPad instance variable.


### Inside your Plugins

You can bind to events in your DocPad plugin. Just add the event handler directly to your plugin’s definition. 

Binding to the `render` event to render from one extension to another would look like so:

``` coffeescript
# Export Plugin
module.exports = (BasePlugin) ->
	# Define Plugin
	class RenderPlugin extends BasePlugin
		# ...

		# Render some content synchronously
		render: (opts) ->
			# Prepare
			{inExtension,outExtension,content} = opts
			docpad = @docpad

			# Perform our rendering
			# ...

```

The context (what `this`/`@` points to) of event handlers in your plugin will be your plugin’s instance.


## Sequence of Events

Events are fired in the following order:

1. `extendTemplateData`
1. `extendCollections`
1. `docpadLoaded`
1. `docpadReady`
1. `docpadDestroy`
1. `consoleSetup`
1. `generateBefore`
1. `populateCollectionsBefore`
1. `populateCollections`
1. `generateAfter`
1. `parseBefore`
1. `parseAfter`
1. `contextualizeBefore`
1. `contextualizeAfter`
1. `renderBefore`
1. `render` (fired for each extension conversion)
1. `renderDocument` (fired for each document render, including layouts and [render passes](/docpad/faq#what-are-render-passes))
1. `renderAfter`
1. `writeBefore`
1. `writeAfter`
1. `serverBefore`
1. `serverExtend`
1. `serverAfter`


## Available Events

### `docpadReady`
Called once DocPad when DocPad is now ready to perform actions which is once it has finished initializing and loading its configuration. Options:
- `docpad` the DocPad instance


### `consoleSetup`
Called once the command line interface when DocPad is loaded. Options:
- `consoleInterface` the console interface instance we are using
- `commander` the instance of [commander](https://github.com/visionmedia/commander.js) we are using


### `generateBefore`
Called just before generating the website.

### `generateAfter`
Called just after generating the website.


### `parseBefore`
Called just before DocPad parses all files.

### `parseAfter`
Called just after DocPad parses all files.


### `renderBefore`
Called just before DocPad renders all the files. Options:
- `collection` a [query-engine](https://github.com/bevry/query-engine) [collection](https://github.com/bevry/query-engine/wiki/Using) containing the models DocPad is about to render
- `templateData` the template data that will be provided to the documents

### `renderAfter`
Called just just after DocPad has rendered all the files. Options:
- `collection` a [query-engine](https://github.com/bevry/query-engine) [collection](https://github.com/bevry/query-engine/wiki/Using) containing the models DocPad rendered

### `render`
Called per document, for each extension conversion. Used to render one extension to another. Options:
- `inExtension` the extension rendering from
- `outExtension` the extension rendering to
- `templateData` the template data that DocPad will use to render the document
- `file` the document’s model instance
- `content` the document’s current content (any updates will overwrite this option)

**Notes:** The file `blah.html.md.eco` will call trigger this event twice. The first time for the `eco` → `md` conversion. The second time for the `md` → `html` conversion.

**Example:** Check the `inExtension` and `outExtension` options to be certain that rendering only occurs for the desired extension conversions. To perform the rendering, write the result back to `opts.content`. 

For example, here’s a `render` event handler that converts the content of files to uppercase when named like `file.txt.captialize|uppercase|upper`:

``` coffeescript
render: (opts) ->
	# Prepare
	{inExtension,outExtension,templateData,file,content} = opts
	docpad = @docpad

	# Render if applicable
	if inExtension in ['capitalize','uppercase','upper'] and outExtension in ['txt']
		opts.content = content.toUpperCase() # your conversion to be saved
```

### `renderDocument`
Called per document, after all extensions have been rendered. Used to perform transformations on the entire document. Options:
- `extension` the resulting extension for our document
- `templateData` the template data that DocPad will use to render this document
- `file` the document’s model instance
- `content` the document’s current content (any updates will overwrite this option)

**Notes:** This event is also called for each **layout** rendering for the document, as well as for each [render pass](/docpad/faq#what-are-render-passes). As such, take care to ensure that your code doesn’t re-transform an already transformed part.

**Example:** [The Pygments Plugin](http://docpad.org/plugin/pygments) more or less uses this event to search for all `<code>` HTML with the CSS class `highlight` (e.g. `<code class="highlight">`), and replaces the element with one that has been syntax highlighted by the popular [pygments](http://pygments.org/) syntax highlighting engine.



### `writeBefore`
Called just before DocPad begins writing all the files. Options:
- `collection` a [query-engine](https://github.com/bevry/query-engine) [collection](https://github.com/bevry/query-engine/wiki/Using) containing the models about to be written
- `templateData` the template data that was provided to the documents

### `writeAfter`
Called just after DocPad has written all the files. Options:
- `collection` a [query-engine](https://github.com/bevry/query-engine) [collection](https://github.com/bevry/query-engine/wiki/Using) containing the models just written


### `serverBefore`
Called just before server setup.

### `serverAfter`
Called just after server setup. Often used to extend the server with routes that will be triggered after the DocPad routes. Options:
- `server` the [express.js](http://expressjs.com) server instance we are using

### `serverExtend`
Called during server setup, and just before the DocPad routes are applied. Used to extend the server with routes that will be triggered before the DocPad routes. Options:
- `server` the [express.js](http://expressjs.com) server instance we are using
