```
title: "Install"
```

_If you are upgrading from one major version to another, be sure to checkout our [Upgrade Guide](/docpad/upgrade) for information relating to backwards compatibility breaks._

1. [Install Node.js & Other Dependencies](/node/install)

1. Ensure NPM is the latest version

	``` bash
	npm install -fg npm
	```

1. Install DocPad

	``` bash
	npm install -fg docpad@6.27
	```

1. If you're upgrading, run this inside your project directory to ensure you get the latest plugin versions

	``` bash
	rm -Rf node_modules; npm install -f
	```

1. If you want operating system notifications, follow [these additional instructions](https://github.com/visionmedia/node-growl#install) - ignore the install npm instructions as we already completed them earlier

_If you get any errors, try running docpad anyway (most installation errors are non fatal and just for debugging purposes) - if you do get a fatal error then refer to our [Troubleshooting Guide](/docpad/troubleshoot) as it is probably easily fixed. :)._
