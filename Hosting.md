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

Works great with [no.de](http://no.de/) and [nodester](http://nodester.com/)

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

	# -------------------------------------
	# Server

	# Configuration
	masterPort = process.env.PORT || 10113

	# Create Instances
	docpadInstance = docpad.createInstance port: masterPort

	# Fetch Servers
	docpadInstance.generateAction -> docpadInstance.serverAction ->
		docpadServer = docpadInstance.server

		# Master Server
		masterServer = docpadServer

		# DNS Servers
		masterServer.use express.vhost 'balupton.*', docpadServer
		masterServer.use express.vhost 'balupton.*.*', docpadServer

	```

3. Customise the _DNS Servers_ part to match your own

	``` coffeescript
	# DNS Servers
	masterServer.use express.vhost 'balupton.*', docpadServer
	masterServer.use express.vhost 'balupton.*.*', docpadServer
	```

4. If you want to use a custom domain:

	1. Ping your server e.g. `ping balupton.no.de`

	2. Grab the IP address from the output

	3. Login to your domain's DNS manager

	4. Create an A Record for your domain pointing to that IP address
