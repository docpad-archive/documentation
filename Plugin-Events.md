These are the plugin events at your disposal.

``` coffeescript

###
Generate Before
Called just before we start generating your website.
###
generateBefore: ({},next) ->
	return next?()

###
Generate After
Called just after we've finished generating your website.
###
generateAfter: ({},next) ->
	return next?()


###
Clean Before
Called just before we start cleaning/preparing the database.
###
cleanBefore: ({},next) ->
	return next?()

###
Clean After
Called just after we've finished cleaning/preparing the database.
###
cleanAfter: ({},next) ->
	return next?()


###
Parse Before
Called just before we start to parse all the files.
###
parseBefore: ({},next) ->
	return next?()

###
Parse After
Called just after we've finished parsing all the files.
###
parseAfter: ({},next) ->
	return next?()


###
Render Before
Called just before we start rendering all the files.
###
renderBefore: ({templateData},next) ->
	return next?()

###
Render
Called per file, for each extension conversion.
Used to render from one extension to another.

Example:
For instance blah.html.md.eco will call this twice:
first for the eco -> md conversion
then again for the md -> html conversion

Usage:
You will likely want to check the inExtension and outExtension arguments against what extensions are expecting for your particular conversion.
You would read the content opts argument, and write your changes back to it.
This can process can be seen below.
###
render: (opts, next) ->
	{inExtension,outExtension,templateData,file,content} = opts
	if inExtension in ['capitalize','uppercase','upper'] and outExtension in ['txt']
		opts.content = content.toUpperCase() # your conversion to be saved
	return next?()


###
Render Document
Called per file, after all the extensions are rendered.
It is also called for each of the layout renderings for the document, as such care should be taken with ensuring your transformation does not re-transform an already transformed part.
Used to perform transformations to the entire document.
Available from DocPad v3.3 and above.

Example:
For instance, you want to search for all code snippets with the class highlight in order to syntax highlight them on the server-side

Usage:
You would read the content opts argument, and write your changes back to it.
###
renderDocument: ({extension,templateData,file}, next) ->
	return next?()

###
Render After
Called just after all the file renderings have finished.
###
renderAfter: ({},next) ->
	return next?()


###
Write Before
Called just before we start writing all the files.
###
writeBefore: ({},next) ->
	return next?()

###
Write Before
Called just after we've wrote all the files.
###
writeAfter: ({},next) ->
	return next?()


###
Server Before
Called just before we start setting up the server.
###
serverBefore: ({},next) ->
	return next?()

###
Server Before
Called just after we finished setting up the server.
###
serverAfter: ({server},next) ->
	return next?()

```