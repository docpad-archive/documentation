
The following events are at your disposal in DocPad v3.3. 

``` coffeescript

###
Generate Before
Called just before we start generating your website
###
generateBefore: ({},next) ->
	return next?()

###
Generate After
Called just after we've finished generating your website
###
generateAfter: ({},next) ->
	return next?()


###
Clean Before
Called just before we start cleaning/preparing the database
###
cleanBefore: ({},next) ->
	return next?()

###
Clean After
Called just after we've finished cleaning/preparing the database
###
cleanAfter: ({},next) ->
	return next?()


###
Parse Before
Called just before we start to parse all the files
###
parseBefore: ({},next) ->
	return next?()

###
Parse After
Called just after we've finished parsing all the files
###
parseAfter: ({},next) ->
	return next?()


###
Render Before
Called just before we start rendering all the files
###
renderBefore: ({templateData},next) ->
	return next?()

###
Render Extension
Called per file, for each extension conversion
Used to render from one extension to another

Example:
For instance blah.html.md.eco will call this twice:
first for the eco -> md conversion
then again for the md -> html conversion

Usage:
You will likely want to check the inExtension and outExtension arguments
against what extensions are expecting for your particular conversion.
You would apply the conversion to the file.content value
and save the results of the conversion back to the file.content variable
###
renderExtension: ({inExtension,outExtension,templateData,file}, next) ->
	return next?()


###
Render Document
Called per file, after all the extensions are rendered
Used to perform alterations to rendered content that are not extension conversions

Example:
For instance, you want to search for all code snippets with the class highlight
in order to syntax highlight them on the server-side

Usage:
You would apply your modifications to the file.content value
and save the results back to the file.content variable
###
renderDocument: ({extension,templateData,file}, next) ->
	return next?()

###
Render After
Called just after all the file renderings have finished
###
renderAfter: ({},next) ->
	return next?()


###
Write Before
Called just before we start writing all the files
###
writeBefore: ({},next) ->
	return next?()

###
Write Before
Called just after we've wrote all the files
###
writeAfter: ({},next) ->
	return next?()


###
Server Before
Called just before we start setting up the server
###
serverBefore: ({},next) ->
	return next?()

###
Server Before
Called just after we finished setting up the server
###
serverAfter: ({server},next) ->
	return next?()

```