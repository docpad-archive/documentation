<style type="text/css">

.flow-num{
	padding: 3px 7px;
	background: orange;
	border-radius: 3px;
	margin: 0;
	font-weight: bold;
	color: #FFF;
	box-shadow: 1px 1px rgb(214, 149, 28);
}

.flow-order{
	padding: 3px 7px;
	background: #259dcf;
	border-radius: 3px;
	margin: 0;
	color: #fff;
	box-shadow: 1px 1px #468DAC;
}

.info-inlay{
	padding: 7px 5px 8px 4px;
	background: #E6E6E6;
	border-radius: 3px;
	border: 1px solid #C9C9C9;
	box-shadow: -1px -1px rgba(111,111,111,0.4);
}

</style>


## Using Events

### Event Handler Structure

Event handlers in DocPad receive two arguments. The first is `opts` which is an object filled with properties that the event may provide to you. The second is `next` which is a completion callback. Both arguments are optional.

Events are fired in a synchronous serial fashion, meaning fire the first handler, wait for it to finish, fire the next handler, wait for it to finish, and so on.

Omitting the `next` callback is perfectly valid and encouraged when you are writing synchronous code. Synchronous code is code that runs everything from start to finish in one go. Asynchronous code however is code that will run a portion at one time, and another portion at another time. With asynchronous code a completion callback is necessary for us to know when everything has properly run, or rather when it is okay to proceed to the next task (or in this case event handler).


### Inside your Configuration File

You can bind to events inside your DocPad configuration file by adding them to the `events` property. Using a `docpad.coffee` file for our configuration, binding to the `serverExtend` event would look like so:

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

The context (what `this`/`@` points to) of event handlers is a shared object between the event handlers that contains only the docpad instance variable.


### Inside your Plugins

You can bind to events inside your DocPad plugin by just adding the event handler directly to your plugin's definition. As such, binding to the `render` event to render from one extension to the other would look like so:

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

The context (what `this`/`@` points to) of event handlers in your plugin will be your plugin's instance.


## Flow of Events

Events are fired in the following order:

1. `extendTemplateData`
- `extendCollections`
- `docpadLoaded`
- <a href="#docpadReady">`docpadReady`</a>
- `docpadDestroy`
- <a href="#consoleSetup">`consoleSetup`</a>
- <a href="#generateBefore">`generateBefore`</a>
- `populateCollectionsBefore`
- `populateCollections`
- <a href="#generateAfter">`generateAfter`
- <a href="#parseBefore">`parseBefore`
- <a href="#parseAfter">`parseAfter`
- `contextualizeBefore`
- `contextualizeAfter`
- <a href="#renderBefore">`renderBefore`
- <a href="#render">`render` (fired for each extension conversion)
- <a href="#renderDocument">`renderDocument` (fired for each document render, including layouts and [render passes](/docpad/faq#what-are-render-passes))
- <a href="#renderAfter">`renderAfter`
- <a href="#writeBefore">`writeBefore`
- <a href="#writeAfter">`writeAfter`
- <a href="#serverBefore">`serverBefore`
- <a href="#serverExtend">`serverExtend`
- <a href="#serverAfter">`serverAfter`


## Available Events

### <a id="docpadReady">`docpadReady`</a> <span class="info-inlay"><span class="flow-order">Flow Order</span> <span class="flow-num">4</span></span>
Called once DocPad when DocPad is now ready to perform actions which is once it has finished initializing and loading its configuration. Options:
- `docpad` the docpad instance


### <a id="consoleSetup">`consoleSetup`</a> <span class="info-inlay"><span class="flow-order">Flow Order</span> <span class="flow-num">6</span></span>
Called once the command line interface for DocPad has loaded. Options:
- `consoleInterface` the console interface instance we are using
- `commander` the instance of [commander](https://github.com/visionmedia/commander.js) we are using


### <a id="generateBefore">`generateBefore`</a> <span class="info-inlay"><span class="flow-order">Flow Order</span> <span class="flow-num">7</span></span>
Called just before we start generating your website

### <a id="generateAfter">`generateAfter`</a> <span class="info-inlay"><span class="flow-order">Flow Order</span> <span class="flow-num">10</span></span>
Called just after we've finished generating your website


### <a id="parseBefore">`parseBefore`</a> <span class="info-inlay"><span class="flow-order">Flow Order</span> <span class="flow-num">11</span></span>
Called just before we start to parse all the files

### <a id="parseAfter">`parseAfter`</a> <span class="info-inlay"><span class="flow-order">Flow Order</span> <span class="flow-num">12</span></span>
Called just after we've finished parsing all the files


### <a id="renderBefore">`renderBefore`</a>
Called just before we start rendering all the files. Options:
- `collection` a [query-engine](https://github.com/bevry/query-engine) [collection](https://github.com/bevry/query-engine/wiki/Using) containing the models we are about to render
- `templateData` the template data that will be provided to the documents

### <a id="renderAfter">`renderAfter`</a>
Called just just after we've rendered all the files. Options:
- `collection` a [query-engine](https://github.com/bevry/query-engine) [collection](https://github.com/bevry/query-engine/wiki/Using) containing the models we've rendered

### <a id="render">`render`</a>
Called per document, for each extension conversion. Used to render one extension to another. Options:
- `inExtension` the extension we are rendering from
- `outExtension` the extension we are rendering to
- `templateData` the template data that we will use for this document's rendering
- `file` the model instance for the document we are rendering
- `content` the current content that this document contains, you shall overwrite this option with any updates you do

Notes: The file `blah.html.md.eco` will call trigger this event twice. The first time for the `eco` to `md` conversion. The second time for the `md` to `html` conversion.

Example: You would check the `inExtension` and `outExtension` options to make sure we only apply our rendering for the desired extension conversions. To apply the rendering, we would write our result back to `opts.content`. For example here is a render event handler that will convert the content of files to upper case when named like `file.txt.captialize|uppercase|upper`:

``` coffeescript
render: (opts) ->
	# Prepare
	{inExtension,outExtension,templateData,file,content} = opts
	docpad = @docpad

	# Render if applicable
	if inExtension in ['capitalize','uppercase','upper'] and outExtension in ['txt']
		opts.content = content.toUpperCase() # your conversion to be saved
```

### <a id="renderDocument">`renderDocument`</a>
Called per document, after all the extensions have been rendered. Used to perform transformations to the entire document. Options:
- `extension` the resulted extension for our document
- `templateData` the template data that we will use for this document's rendering
- `file` the model instance for the document we are rendering
- `content` the current content that this document contains, you shall overwrite this option with any updates you do

Notes: It is also called for each of the layout rendering for the document, as well as for each [render pass](/docpad/faq#what-are-render-passes), as such care should be taken with ensuring your transformation does not re-transform an already transformed part.

Example: [The Pygments Plugin](https://github.com/docpad/docpad-plugin-pygments/blob/master/src/pygments.plugin.coffee#L1) more or less uses this event to search for all `<code>` HTML elements that have the CSS class `highlight` (e.g. `<code class="highlight">`) and replaces the element with one that has been syntax highlighted by the popular [pygments](http://pygments.org/) syntax highlighting engine.



### <a id="writeBefore">`writeBefore`</a>
Called just before we start writing all the files. Options:
- `collection` a [query-engine](https://github.com/bevry/query-engine) [collection](https://github.com/bevry/query-engine/wiki/Using) containing the models we are about to write
- `templateData` the template data that was provided to the documents

### <a id="writeAfter">`writeAfter`</a>
Called just just after we've wrote all the files. Options:
- `collection` a [query-engine](https://github.com/bevry/query-engine) [collection](https://github.com/bevry/query-engine/wiki/Using) containing the models we are about to render


### <a id="serverBefore">`serverBefore`</a>
Called just before we start setting up the server

### <a id="serverAfter">`serverAfter`</a>
Called just after we finished setting up the server. Often used to extend the server with routes that will be triggered after the DocPad routes. Options:
- `server` the [express.js](http://expressjs.com/) server instance we are using

### <a id="serverExtend">`serverExtend`</a>
Called just while we are setting up the server, and just before the DocPad routes are applied. Used to extend the server with routes that will be triggered before the DocPad routes. Options:
- `server` the [express.js](http://expressjs.com/) server instance we are using

Example: [The basicAuth Plugin](https://github.com/mikeumus/docpad-plugin-basicauth/blob/master/basicauth.plugin.coffee#L1) uses 'serverExtend' to add express' basicAuth to a route.
