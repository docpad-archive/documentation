```
title: "API"
```

This page will go over using DocPad as a module, and the API available to you.


## Install DocPad

Besides having [Node.js installed](/node/install), you'll want to install DocPad locally to your project, you can do this by running `npm install --save docpad` in your command line. This will install DocPad into `./node_modules/docpad` and make it accessible via [Node.js's require function](http://nodejs.org/docs/latest/api/all.html#all_require) (e.g. `require('docpad')`)

If you are wanting to utilise DocPad for rendering, you'll also want to install some rendering [Plugins](/docpad/plugins).


## Create your DocPad Instance

Firstly, you need to create your DocPad instance, you can do this like so:

``` javascript
var docpadInstanceConfiguration = {};
require('docpad').createInstance(docpadInstanceConfiguration, function(err,docpadInstance){
	if (err)  return console.log(err.stack);
	// ...
});
```


## Rendering individual files

You can use DocPad as a module to render individual files very easily. This allows you to utilise DocPad for all the rendering inside your application, instead of having to _write **and maintain**_ specific wrappers for each rendering engine yourself.

### Render some text with DocPad

``` javascript
var renderOpts = {
	text: 'here is some **markdown**',
	filename:'markdown',
	renderSingleExtensions:true
};
docpadInstance.action('render', renderOpts, function(err,result){
	console.log(result);
});
```

### Render a file path with DocPad

``` javascript
var renderOpts = {
	path: '/some/file.html.md',
	renderSingleExtensions:true
};
docpadInstance.action('render', renderOpts, function(err,result){
	console.log(result);
});
```


## DocPad CLI Actions

Here is how you would normalise common tasks you would typically achieve with the DocPad command line interface.

### Performing a generation

``` javascript
docpadInstance.action('generate', function(err,result){
	if (err)  return console.log(err.stack);
	console.log('OK');
});
```


### Start the DocPad server

``` javascript
docpadInstance.action('server', function(err,result){
	if (err)  return console.log(err.stack);
	console.log('OK');
});
```

### Generate and Start the DocPad Server

You can combine actions by separating them with a space, like so:

``` javascript
docpadInstance.action('generate server', function(err,result){
	if (err)  return console.log(err.stack);
	console.log('OK');
});
```

### Perform an initial generation, then watch files and regenerate when a change occurs

``` javascript
docpadInstance.action('generate watch', function(err,result){
	if (err)  return console.log(err.stack);
	console.log('OK');
});
```


## Using the Database

DocPad using [Backbone.js](http://documentcloud.github.com/backbone/) for its Models, and [QueryEngine](https://github.com/bevry/query-engine) for its Collections. Providing a powerful database that you can query in a noSQL type fashion. You can discover the entire query API on the [Using QueryEngine](https://github.com/bevry/query-engine/wiki/Using) wiki page.

### Create a Document

``` javascript
document = docpadInstance.createDocument(data, options)
```

### Get the database

``` javascript
database = docpadInstance.getDatabase()
```

### Querying

``` javascript
// Get files, returns a cached live collection
resultCollection = docpadInstance.getFiles(query, sorting, paging)

// Get a file
resultModel = docpadInstance.getFile(query, sorting, paging)

// Get files at path (forwards onto getFiles)
resultCollection = docpadInstance.getFilesAtPath(path, sorting, paging)

// Get a file at a relative or absolute path or url
resultModel = docpadInstance.getFileAtPath(path, sorting, paging)

// Get a file by its id
resultModel = docpadInstance.getFileById(id, {collection:null})

// Get a file by a route, useful when doing server requests
docpadInstance.getFileByRoute(url, function(err, resultModel){
	if ( err )  console.log(err.stack)
})
```

[For more information about Querying, check out this FAQ Entry.](/docpad/faq#what-is-findalllive)



## Using with Express

If you already have an Express.js application, you can do the following to just stick DocPad straight ontop of it:

``` javascript
// Create Server and Express Application
var express = require('express');
var http = require('http');
var app = express();
var server = http.createServer(app).listen(8080);

// Add our Application Middlewares
app.use(app.router);

// Add DocPad to our Application
var docpadInstanceConfiguration = {
	// Give it our express application and http server
	serverExpress: app,
	serverHttp: server,
	
	// Tell it not to load the standard middlewares (as we handled that above)
	middlewareStandard: false
};
var docpadInstance = require('docpad').createInstance(docpadInstanceConfiguration, function(err){
	if (err)  return console.log(err.stack);
	// Tell DocPad to perform a generation, extend our server with its routes, and watch for changes
	docpadInstance.action('generate server watch', function(err){
		if (err)  return console.log(err.stack);
	});
});

// Continue with your application
// ...
```

Here is some code for manually rendering a document (documents are files inside `src/documents`) with a custom route:

``` coffee
app.get '/alias-for-home', (req,res,next) ->
	req.templateData = {
		weDidSomeCustomRendering: true
	};
	var document = docpadInstance.getFile({relativePath:'home.html.md'});
	docpadInstance.serveDocument({document, req, res, next});
```
