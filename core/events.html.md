## Using Events

### Event Handler Structure

All DocPad events receive two arguments (both optional): 

1. `opts`, an simple object containing any options that the event provides
1. `next`, a completion callback

DocPad's events are fired in a *synchronous* (or *serial*) fashion. In other words, when the first event runs until finished, then the next event fires and runs until finished, and so on. 

*Asynchronous* code, however, has no implicit guarantees about the order of execution. It will fire the first event, and may then immediately fire the second event while the first is still running. 

That's why asynchronous code requires callbacks. When the first event is done, it will run the callback function it was invoked with.  It's the callback's job to signal when it's okay to proceed to the next event. 

Node.js itself is built for asynchronous execution, so it's pretty common for Node.js programs to run asynchronously. 

Since DocPad's events are run synchronously, omitting the `next` callback is perfectly valid (even encouraged) if you're using DocPad in your own synchronous code. (Of course, you're free to write in whatever style works best for you! If you enjoy coding in the asynchronous style, the `next` callback is available for you.)


### Inside your Configuration File

You can bind to events in your DocPad configuration file by adding them to the `events` property. 

**Example:** Let's use a `docpad.coffee` configuration file. Binding to the `serverExtend` event would look like so:

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


## Available Events

Sorted by their flow of execution within DocPad


### `extendTemplateData`
Called each time the configuration for DocPad reloads. Called after most of the configuration has loaded and when it is time to extend our template data.

**Options:**
- `templateData` the object to inject your additions to

Use to inject new template data variables and helpers into the template data.

**Examples:**
- [Services Plugin](/plugin/services)
- [Feedr Plugin](/plugin/feedr)


### `extendCollections`
Called each time the configuration for DocPad reloads. Called after most of the configuration has loaded and when it is time to extend our collections.

Use to create additional collections.

**Examples:**
- [Partials Plugin](/plugin/partials)



### `docpadLoaded`
Called each time the configuration for DocPad reloads. Called before `docpadReady` as we have to load the configuration in order to be ready.



### `docpadReady`
Called once DocPad when DocPad is now ready to perform actions which is once it has finished initializing and loading its configuration. Partnered with the `docpadDestroy` event.


### `consoleSetup`
Called once the command line interface for DocPad has loaded.

**Options:**
- `consoleInterface` the console interface instance we are using
- `commander` the instance of [commander](https://github.com/visionmedia/commander.js) we are using

Use to extend the console interface with additional commands.

**Examples:**
- [GitHub Pages Plugin](/plugin/ghpages)



### `populateCollectionsBefore`
Called just before we start to insert dynamic files into the database. Called before each generation, just before the `generateBefore` event. Partnered with the `populateCollections` event.

### `populateCollections`
Called just after we've inserted dynamic files into the collections. Called before each generation, just before the `generateBefore` event. Partnered with the `populateCollectionsBefore` event.

Use this for inserting your dynamic files into the database.

**Examples:**
- [Tumblr Importer Plugin](/plugin/tumblr)



### `generateBefore`
Called just before we start generating your project. Partnered with the `generateAfter` event.

**Options:**
- `reset` whether or not this is a partial- (`false`) or full-regeneration (`true`)
- <del><code>server</code></del> 
  <ins>Deprecated; use `getServer()` API method instead</ins>


### <del><code>parseBefore</code></del>
<ins>Deprecated/removed since DocPad v6.58.0.</ins> 
See [issue #736](https://github.com/bevry/docpad/issues/736) for information.

### <del><code>parseAfter</code></del>
<ins>Deprecated/removed since DocPad v6.58.0.</ins> 
See [issue #736](https://github.com/bevry/docpad/issues/736) for information.


### `conextualizeBefore`
Called just before we start to contextualize all the files. Partnered with the `contextualizeAfter` event. Contextualizing is the process of adding layouts and awareness of other documents to our document.

**Options:**
- `collection` the collection we are working with
- <del><code>templateData</code></del>
  <ins>Deprecated; use `extendTemplateData` event instead</ins>

### `contextualizeAfter`
Called just after we've finished contextualize all the files. Partnered with the `conextualizeBefore` event. Contextualizing is the process of adding layouts and awareness of other documents to our document.

**Options:**
- `collection` the collection we are working with
- <del><code>templateData</code></del>
  <ins>Deprecated; use `extendTemplateData` event instead</ins>



### `renderBefore`
Called just before we start rendering all the files. Partnered with the `renderAfter` event.

**Options:**
- `collection` a [query-engine][] [collection][] containing the models we are about to render
- `templateData` the template data that will be provided to the documents



### `renderCollectionBefore`
Triggered before a render collection is about to be rendered. Added by [Bruno Heridet](https://github.com/Delapouite) with [Pull Request #608](https://github.com/bevry/docpad/pull/608).

**Options:**
- `collection` a [query-engine][] [collection][] containing the models we are about to render
- `renderPass` which render pass is this render collection for?


### `renderCollectionAfter`
Triggered before a render collection is about to be rendered. Added by [Bruno Heridet](https://github.com/Delapouite) with [Pull Request #608](https://github.com/bevry/docpad/pull/608).

**Options:**
- `collection` a [query-engine][] [collection][] containing the models we are about to render
- `renderPass` which render pass is this render collection for?



### `render`
Called per document, for each extension conversion.

Use to render one extension to another.

**Options:**
- `inExtension` the extension we are rendering from
- `outExtension` the extension we are rendering to
- `templateData` the template data that we will use for this document's rendering
- `file` the model instance for the document we are rendering
- `content` the current content that this document contains, you shall overwrite this option with any updates you do

**Notes:** The file `blah.html.md.eco` will call trigger this event twice. The first time for the `eco` to `md` conversion. The second time for the `md` to `html` conversion.

**Example:** You would check the `inExtension` and `outExtension` options to make sure we only apply our rendering for the desired extension conversions. To apply the rendering, we would write our result back to `opts.content`. For example here is a render event handler that will convert the content of files to upper case when named like `file.txt.captialize|uppercase|upper`:

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
Called per document, after all the extensions have been rendered.

Use to perform transformations to the entire document.

**Options:**
- `extension` the resulted extension for our document
- `templateData` the template data that we will use for this document's rendering
- `file` the model instance for the document we are rendering
- `content` the current content that this document contains, you shall overwrite this option with any updates you do

**Notes:** It is also called for each of the layout rendering for the document, as well as for each [render pass](/docpad/faq#what-are-render-passes), as such care should be taken with ensuring your transformation does not re-transform an already transformed part.

**Example:** [The Pygments Plugin](http://docpad.org/plugin/pygments) more or less uses this event to search for all `<code>` HTML elements that have the CSS class `highlight` (e.g., `<code class="highlight">`) and replaces the element with one that has been syntax highlighted by the popular [pygments](http://pygments.org) syntax highlighting engine.


### `renderAfter`
Called just just after we've rendered all the files. Partnered with the `renderBefore` event.

**Options:**
- `collection` a [query-engine][] [collection][] containing the models we've rendered



### `writeBefore`
Called just before we start writing all the files. Partnered with the `writeAfter` event.

**Options:**
- `collection` a [query-engine][] [collection][] containing the models we are about to write
- `templateData` the template data that was provided to the documents


### `writeAfter`
Called just just after we've wrote all the files. Partnered with the `writeBefore` event.

**Options:**
- `collection` a [query-engine][] [collection][query-engine collection] containing the models we are about to render



### `generateAfter`
Called just after we've finished generating your project.  Partnered with the `generateBefore` event.


### `generated`
Called just after the initial generation has completed.



### `serverBefore`
Called just before we start setting up the server. Partnered with the `serverAfter` event.


### `serverExtend`
Called just while we are setting up the server, and just before the DocPad routes are applied.

Use to extend the server with routes that will be triggered before the DocPad routes.

**Options:**
- `server` and `serverExpress` are the [Express.js][] server instance we are using
- `serverHttp` is the raw Node.js HTTP server we are using
- `express` is the Express module we are using


### `serverAfter`
Called just after we finished setting up the server.

Use to extend the server with routes that will be triggered after the DocPad routes.

**Options:**
- `server` and `serverExpress` are the [Express.js][] server instance we are using
- `serverHttp` is the raw Node.js HTTP server we are using
- `express` is the Express module we are using



### `docpadDestroy`
Called when it is time for DocPad to shutdown.  Partnered with the `docpadReady` event.

Use this to shutdown anything inside your plugins, close all connections, file system handlers, files, etc.

[query-engine]: https://github.com/bevry/query-engine
[query-engine collection]: https://github.com/bevry/query-engine/wiki/Using
[Express.js]: http://expressjs.com