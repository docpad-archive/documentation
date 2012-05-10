DocPad websites can be hosted anywhere as they are just a generated static website, nothing special about them at all (well besides them being awesome!).

Here is how you can host them on several different server types.



### Via a Standard Apache Server

Upload the generated `mywebsite/out` directory to your apache server's `public_html` or `htdocs` directory :)



### Via GitHub Pages

1. [Follow these instructions to get setup with your GitHub Pages Repository](https://github.com/blog/272-github-pages)
2. Copy the generated `mywebsite/out` directory to your repository.
3. Push the repository to GitHub

__(I'll admit, this isn't as nice as it could be, will improve this in future versions)__



### Via a Node.js Hosting Provider

Works great with [Heroku](http://www.heroku.com/), [Nodester](http://nodester.com/) and [no.de](http://no.de/)

Inside your website's directory:

1. Create a `config.json` file which contains:

	``` javascript
	{"version":"latest"}
	```

1. Create a `Procfile` which contains:

	``` javascript
	web: node server.js
	```

1. Inside your website's `package.json` file, ensure it has the following dependencies. Set the DocPad version to whichever version you are using, keep it specific.

	``` javascript
	"dependencies": {
		"coffee-script": "1.2.x",
		"express": "2.5.x",
		"docpad": "3.2.7"
	},
	```

1. Create a `server.js` file which contains:

	``` javascript
	require('coffee-script');
	require(require('path').join(__dirname,'server.coffee'));
	```

1. Create a `server.coffee` file, [base it off the one inside the KitchenSink Skeleton.](https://github.com/bevry/kitchensink.docpad/blob/master/server.coffee)

	1. Be sure to change vhosts part to the domains that you will be using

1. If you are going to be using a custom domain name:

	1. Ping your server e.g. `ping balupton.no.de`

	1. Grab the IP address from the output

	1. Login to your domain's DNS manager

	1. Create an A Record for your domain pointing to that IP address

1. Do a deploy to your server. For the instructions on how to do this, refer to your hosting providers guide.

	1. [Here is the guide for Heroku](http://devcenter.heroku.com/articles/node-js)
