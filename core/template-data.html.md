```
title: "Template Data & Helpers"
```

## Standard Template Data

- `site` &mdash; an object of several site-specific properties, contains:
	- `date` &mdash; a JavaScript `Date` object of when the site was last generated
- `document` &mdash; a JavaScript `Object` containing the serialised values of the `documentModel` (e.g. `documentModel.toJSON()`)
- `req` &mdash; dynamic documents will also have this available; it’s a reference to the current request (`req`) object  created by the [ExpressJS](http://expressjs.com) server

## Standard Template Helpers

- `getEnvironment()` &mdash; a string of the current environment(s) DocPad is running under
- `getEnvironments()` &mdash; an array of the current environments DocPad is running under
- `referencesOthers()` &mdash; if called, sets the document’s `referenceOthers` [meta data](/docpad/meta-data) property to `true`
- `getDocument()` &mdash; a reference to the current document being rendered; documents are defined by the [Document Class](https://github.com/bevry/docpad/blob/master/src/lib/models/document.coffee), which extends the [File Class](https://github.com/bevry/docpad/blob/master/src/lib/models/file.coffee), which extends a [Backbone Model](http://documentcloud.github.com/backbone/#Model)
- `getPath(path,parentPath)` gets a path relative to the current document
- `getFiles(query,sorting,paging)` gets all files that match the arguments, and caches the resulting collection
- `getFile(query,sorting,paging)` gets a single file that matches the arguments
- `getFilesAtPath(relativePath)` gets a file at the given path (processed via `getPath()`)
- `getDatabase()` &mdash; a [Query-Engine](https://github.com/bevry/query-engine) collection of all our documents
- `getCollection(collectionName)` &mdash; a [Query-Engine](https://github.com/bevry/query-engine) collection of a particular sub-collection, built in collections are:
	- `documents` &mdash; for all documents
	- `files` &mdash; for all non-rendered files
	- `layouts` &mdash; for all layout files
	- `html` &mdash; for all documents and files that result in an HTML file
	- `stylesheet` &mdash; for all stylesheet files (including CSS pre-processors)
- `getBlock(blockName)` &mdash; valid block names are:
	- `scripts` &mdash; a collection of scripts to be output
	- `styles` &mdash; a collection of styles to be output
	- `meta` &mdash; a collection of meta data to be output
- `include(relativePath)` returns the contents the file at `relativePath`
