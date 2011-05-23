Post your DocPad tips and tricks here.

### Using FilePad as a CMS for DocPad

[FilePad](https://github.com/balupton/filepad) is a local file browser and editor in your browser. It also utilises [NowPad](github.com/balupton/nowpad) for realtime collaborative editing.

You can use it to provide a browser editing interface for your docpad src directory. Here's the steps:

- Via the command line:

		npm install -g docpad
		npm install -g filepad
		mkdir mywebsite
		cd mywebsite
		filepad src &
		docpad

- Via CoffeeScript

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

Because docpad watches the src directory for changes, whenever you save a change with filepad, your docpad website will be automatically regenerated :)
