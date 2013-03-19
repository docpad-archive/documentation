DocPad websites can be deployed anywhere. Here are a few of the most common deployments.


## To a Node.js Hosting Provider



### Inside your website's directory

1. Add the following to your website's `package.json` file. Add all the dependencies you are using and make sure their versions are correct - as well as ensure all commas are correctly placed.

	``` javascript
	"engines" : {
		"node": "0.8.x",
		"npm": "1.2.x"
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

### For deployment to [Heroku]([Heroku](http://www.heroku.com/)

1. Create a `Procfile` file inside your project that contains:

	```
	web: node_modules/docpad/bin/docpad-server
	```

1. Set your heroku instance to run in production mode

	```
	heroku config:add NODE_ENV=production
	```

1. [Follow the rest of the Heroku guide here](http://devcenter.heroku.com/articles/node-js)



### For deployment to [AppFog](https://www.appfog.com/)

1. Create a `app.js` file inside your project that contains:

	``` javascript
	module.exports = require(__dirname+'/node_modules/docpad/out/bin/docpad-server');
	```

1. [Follow the rest of the AppFog guide here](https://docs.appfog.com/getting-started)



### For deployment to [Windows Azure](http://www.windowsazure.com/en-us/home/scenarios/web-sites/)

1. Create a deployment script that triggers the static content generation. To create the script run the following command using the [Windows Azure CLI Tools](http://www.windowsazure.com/en-us/develop/nodejs/how-to-guides/command-line-tools/):

	```
	azure site deploymentscript --basic -t bash
	```

1. Modify the `deploy.sh` file by chaning the `# Deployment` section to the following lines. You can see a complete example of the deploy.sh file [here](https://gist.github.com/ntotten/4715760#file-deploy-sh).

	``` bash
	echo Handling deployment.

	# 1. Install npm packages
	if [ -e "$DEPLOYMENT_SOURCE/package.json" ]; then
	  cd "$DEPLOYMENT_SOURCE"
	  npm install --production --silent
	  exitWithMessageOnError "npm failed"
	  cd - > /dev/null
	fi

	# 2. Build DocPad Site
	echo Building the DocPad site
	cd "$DEPLOYMENT_SOURCE"
	node ./node_modules/docpad/bin/docpad generate
	exitWithMessageOnError "Docpad generation failed"

	# 3. KuduSync
	echo Kudu Sync from "$DEPLOYMENT_SOURCE/out" to "$DEPLOYMENT_TARGET"
	$KUDU_SYNC_COMMAND -q -f "$DEPLOYMENT_SOURCE/out" -t "$DEPLOYMENT_TARGET" -n "$NEXT_MANIFEST_PATH" -p "$PREVIOUS_MANIFEST_PATH" -i ".git;.deployment;deploy.sh" 2> /dev/null
	exitWithMessageOnError "Kudu Sync failed"
	```

1. Last, create a web.config file in the files directory of your site with the URL rewrite rules shown below. These rules remove the html extensions from your urls. You can see the main portions of this web.config file below. You can download the complete file [here](https://gist.github.com/ntotten/4715760#file-web-config).

	``` xml
	<rule name="RemoveHTMLExtensions" stopProcessing="true">
		<match url="^(.*)\.html$" />
		<action type="Redirect" url="{R:1}" appendQueryString="true" />
	</rule>
	<rule name="RewriteHTMLExtensions" stopProcessing="true">
		<match url="(.*)" />
		<conditions>
			<add input="{REQUEST_FILENAME}" matchType="IsFile" negate="true"/>
			<add input="{REQUEST_FILENAME}" matchType="IsDirectory" negate="true"/>
		</conditions>
		<action type="Rewrite" url="{R:1}.html" />
	</rule>
	```
	
1. [Follow the rest of the Azure guide here](http://blog.ntotten.com/2013/01/11/static-site-generation-with-docpad-on-windows-azure-web-sites/)



### For deployment to [Nodejitsu](http://nodejitsu.com/)

1. [Follow the rest of the Nodejitsu guide here](http://nodejitsu.com/paas/getting-started.html)



### Custom domains

If you're also wanting to use custom domains for your website, [follow the Heroku Guide here](https://devcenter.heroku.com/articles/custom-domains), or alternatively here is a generic guide:

1. Ping your server e.g. `ping balupton.herokuapp.com`

1. Grab the IP address from the output

1. Login to your domain's DNS manager

1. Create an A Record for your domain pointing to that IP address



## To Static Servers (Apache, Nginx, etc)

1. Perform a generation for a static production environment using `docpad generate --env static`

2. Upload the generated directory to your server's `public_html` or `htdocs` directory



## To [GitHub Pages](http://pages.github.com/)

1. Install the [GitHub Pages Plugin](http://docpad.org/plugin/ghpages)

	```
	npm install --save docpad-plugin-ghpages
	```

2. Deploy to GitHub Pages using the plugin

	```
	docpad deploy-ghpages
	```


## To a Cloud Data Storage Provider (AWS S3, Google Storage, etc)

1. [Checkout the DocPad Sunny Plugin](https://github.com/bobobo1618/docpad-plugin-sunny)
