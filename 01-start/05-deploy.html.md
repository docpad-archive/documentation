DocPad websites can be deployed anywhere. Here are a few of the most common deployments.


## To a Node.js Hosting Provider

Works great with [Heroku](http://www.heroku.com/), [Nodejitsu](http://nodejitsu.com/),  [AppFog](https://www.appfog.com/), and [Windows Azure](http://www.windowsazure.com/en-us/home/scenarios/web-sites/).

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

1. For deployment to Windows Azure:

	1. Create a deployment script that triggers the static content generation. To create the script run the following command using the [Windows Azure CLI Tools](http://www.windowsazure.com/en-us/develop/nodejs/how-to-guides/command-line-tools/):

		```
		azure site deploymentscript --basic -t bash
		```

	1. Modify the `deploy.sh` file by chaning the `# Deployment` section to the following lines. You can see a complete example of the deploy.sh file [here](https://gist.github.com/ntotten/4715760#file-deploy-sh).

		```
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

	```
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

1. You're now ready to do a deploy to your hosting provider. Follow the guide of your hosting provider in order to do this.

	1. [Here is the guide for Heroku](http://devcenter.heroku.com/articles/node-js)
	1. [Here is the guide for Nodejitsu](http://nodejitsu.com/paas/getting-started.html)
	1. [Here is the guide for AppFog](https://docs.appfog.com/getting-started)
	1. [Here is the guide for Windows Azure](http://blog.ntotten.com/2013/01/11/static-site-generation-with-docpad-on-windows-azure-web-sites/)

1. Optional: If you're also wanting to use a custom domain for your website, [follow the Heroku Guide here](https://devcenter.heroku.com/articles/custom-domains), or alternatively here is a generic guide:

	1. Ping your server e.g. `ping balupton.herokuapp.com`

	1. Grab the IP address from the output

	1. Login to your domain's DNS manager

	1. Create an A Record for your domain pointing to that IP address



## To a Standard Static Server (apache/nginx)

1. Perform a generation for a static production environment using `docpad generate --env static`

2. Upload the generated directory to your server's `public_html` or `htdocs` directory


## To GitHub Pages

1. For GitHub Pages we want our output directory to our website's root directory. To do this, we'll add `outPath: '.'` to our [docpad configuration file](/docpad/config)

2. Perform a generation for an apache and production environment using `docpad generate --env static`

3. Commit your changes to the `gh-pages` branch, and push the branch to github

4. Optional: If you're also wanting to use a custom domain for your website, [follow the GitHub Pages guide here](https://help.github.com/articles/setting-up-a-custom-domain-with-pages)


## To a Cloud Data Storage Provider (AWS S3, Google Storage, etc)

[Checkout the DocPad Sunny Plugin](https://github.com/bobobo1618/docpad-plugin-sunny)
