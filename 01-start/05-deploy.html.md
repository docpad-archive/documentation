DocPad websites can be deployed anywhere. Here are a few of the most common deployments.


## Via a Node.js Hosting Provider

Works great with [Heroku](http://www.heroku.com/), [Nodejitsu](http://nodejitsu.com/) and [AppFog](https://www.appfog.com/).

Inside your website's directory:

1. Add the following to your website's `package.json` file. Add all the dependencies you are using and make sure their versions are correct - as well as ensure all commas are correctly placed.

	``` javascript
	"engines" : {
		"node": "0.8.x",
		"npm": "1.1.x"
	},
	"dependencies": {
		"docpad": "6.x",
		"docpad-plugin-blah": "2.x"
	},
	"main": "node_modules/docpad/bin/docpad-server",
	"scripts": {
		"start": "node_modules/docpad/bin/docpad-server"
	}
	```

1. For deployment to Heroku, you'll have to create a `Procfile` file that contains:

	```
	web: node_modules/docpad/bin/docpad-server
	```

1. For deployment to AppFog, you'll have to create a `app.js` file that contains:
	
	``` javascript
	module.exports = require(__dirname+'/node_modules/docpad/out/bin/docpad-server');
	```

1. Your now ready to do a deploy to your hosting provider. Follow the guide of your hosting provider in order to do this.

	1. [Here is the guide for Heroku](http://devcenter.heroku.com/articles/node-js)
	1. [Here is the guide for Nodejitsu](http://nodejitsu.com/paas/getting-started.html)
	1. [Here is the gude for AppFog](https://docs.appfog.com/getting-started)

1. Optional: If you're also wanting to use a custom domain for your website, [follow the Heroku Guide here](https://devcenter.heroku.com/articles/custom-domains), or alternatively here is a generic guide:

	1. Ping your server e.g. `ping balupton.herokuapp.com`

	1. Grab the IP address from the output

	1. Login to your domain's DNS manager

	1. Create an A Record for your domain pointing to that IP address



## Via a Standard Static Server (apache/nginx)

1. Perform a generation for a static production environment using `docpad generate --env static`

2. Upload the generated directory to your server's `public_html` or `htdocs` directory


## Via GitHub Pages

1. For GitHub Pages we want our output directory to our website's root directory. To do this, we'll add `outPath: '.'` to our [docpad configuration file](/docpad/config)

2. Perform a generation for an apache and production environment using `docpad generate --env static`

3. Commit your changes to the `gh-pages` branch, and push the branch to github

4. Optional: If you're also wanting to use a custom domain for your website, [follow the GitHub Pages guide here](https://help.github.com/articles/setting-up-a-custom-domain-with-pages)