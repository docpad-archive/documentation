```
title: "API"
```

How to use DocPad as a module, and its API.


## Install DocPad

Besides having [Node.js installed](https://github.com/bevry/community/wiki/Installing-Node), you’ll want to install DocPad locally to your project, you can do this by running `npm install -f docpad` in your command line. This will install DocPad into `./node_modules/docpad` and make it accessible via [Node.js's require function](http://nodejs.org/docs/latest/api/all.html#all_require) (e.g. `require('docpad')`)

If you want to utilise DocPad for rendering, you’ll also need to install some rendering [Plugins](/docpad/plugins).


## Create your DocPad Instance

First, you need to create your DocPad instance, like so:

``` javascript
var docpadInstanceConfiguration = {};
require('docpad').createInstance(docpadInstanceConfiguration, function(err,docpadInstance){
	if (err)  return console.log(err.stack);
	// ...
});
```


## Rendering individual files

Using DocPad as a module to render files is easy. You can let DocPad handle rendering for your application, instead of having to write (and maintain) wrappers for each rendering engine yourself.

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

Here’s how to normalise some common tasks you can do with DocPad’s command line interface.

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

You can combine actions by separating them with a space:

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

DocPad uses:

- [Backbone.js](http://documentcloud.github.com/backbone/) for its **Models**, and 
- [QueryEngine](https://github.com/bevry/query-engine) for its **Collections**.

This is the foundation for a powerful database, which takes NoSQL-type queries. You can discover the entire query API on the [Using QueryEngine](https://github.com/bevry/query-engine/wiki/Using) wiki page.

### Create a Document

``` javascript
var document = docpadInstance.createDocument(data,options);
```

### Get the database

``` javascript
var database = docpadInstance.getDatabase();
```

### Query the database

``` javascript
var resultCollection, resultModel;
resultCollection = docpadInstance.getFiles(query,sorting,paging);
resultModel = docpadInstance.getFile(query,sorting,paging);
resultCollection = docpadInstance.getFilesAtPath(path,sorting,paging);
resultModel = docpadInstance.getFileAtPath(path,sorting,paging);
```



## Using with Express

If you already have an Express.js application, you can simply stick DocPad straight on top:

``` javascript
// Create Server and Express Application
var express = require('express');
var http = require('http');
var app = express();
var server = http.createServer(app).listen(8080);

// Add our Application Stuff
app.use(express.bodyParser());
app.use(express.methodOverride());
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

Here’s an example showing how to render a document with a custom route:

``` javascript
app.get '/alias-for-home', (req,res,next) ->
	req.templateData = {
		weDidSomeCustomRendering: true
	};
	var document = docpadInstance.getFile({relativePath:'home.html.md'});
	docpadInstance.serveDocument({document,req,res,next});
```
