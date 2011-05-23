
DocPad websites can be hosted anywhere as they are just a generated static website, nothing special about them at all (well besides them being awesome!).

Here is how you can host them on several different server types.



### Via a Standard Apache Server

Upload the generated `mywebsite/out` directory to your apache server's `public_html` or `htdocs` directory :)



### Via GitHub Pages

1. [Follow these instructions to get setup with your GitHub Pages Repository](https://github.com/blog/272-github-pages)
2. Copy the generated `mywebsite/out` directory to your repository.
3. Push the repository to GitHub

__(I'll admit, this isn't as nice as it could be, will improve this in future versions)__



### Via a Node.js Server

Works great with [Nodester](http://nodester.com/) and [DuoStack](https://www.duostack.com/)

1. Create a `server.js` file which contains:

	``` javascript
	require('coffee-script');
	require(__dirname+'/server.coffee');
	```

2. Create a `server.coffee` file which contains:

	``` coffeescript
	# Requires
	docpad = require 'docpad'
	express = require 'express'

	# Create Instances
	docpadInstance = docpad.createInstance port:8002

	# Fetch Servers
	docpadServer = docpadInstance.server

	# Master Server
	app = express.createServer()
	app.use express.vhost 'balupton.*', docpadServer
	app.listen process.env.PORT || 8001
	```

3. Adjust the vhost domain and the port number with your own



### Via a Node.js Server with FilePad as a CMS

Works great with [no.de](http://no.de/)

1. Install MongoDB on your server

	- [Here are the instructions if you're using no.de](http://wiki.joyent.com/display/node/Installing+MongoDB+on+a+Node+SmartMachine)

2. Create a `server.js` file which contains:

	``` javascript
	require('coffee-script');
	require(__dirname+'/server.coffee');
	```

3. Create a `server.coffee` file which contains:

	``` coffeescript
	# Requires
	docpad = require 'docpad'
	filepad = require 'filepad'
	express = require 'express'

	# Create Instances
	docpadInstance = docpad.createInstance port:8002
	filepadInstance = filepad.createInstance path: __dirname+'/src', port:8003

	# Fetch Servers
	docpadServer = docpadInstance.server
	filepadServer = filepadInstance.server

	# Master Server
	app = express.createServer()
	app.use express.vhost 'mywebsite.*', docpadServer
	app.use express.vhost 'edit.mywebsite.*', filepadServer
	app.listen process.env.PORT || 8080
	```
