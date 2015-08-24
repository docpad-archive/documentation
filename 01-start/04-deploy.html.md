DocPad websites can be deployed anywhere. Here are a few of the most common deployments.



## Deploying DocPad

### Preparing DocPad for Deployment

1. Ensure your project's `package.json` file contains the following:

	``` javascript
	"engines" : {
		"node": "0.12",
		"npm": "2"
	},
	"dependencies": {
		"docpad": "6",
		"docpad-plugin-blah": "2"
	},
	"main": "node_modules/.bin/docpad-server",
	"scripts": {
		"start": "node_modules/.bin/docpad-server",
		"test": "node_modules/.bin/docpad generate --debug --silent",
		"info": "node_modules/.bin/docpad info --silent"
	}
	```
	
	Correct dependencies with what you are actually using.


## To Static Servers (Apache, Nginx, etc.)


### For deployment to a Custom Static Server

1. Perform a generation for a static production environment using `docpad generate --env static`

2. Upload the generated directory to your server's `public_html` or `htdocs` directory

	1. If you use rsync, [checkout our DocPad rsync deploy script](https://gist.github.com/Hypercubed/5804999)



### For deployment to [GitHub Pages](http://pages.github.com)

1. Install the [GitHub Pages Plugin](/plugin/ghpages)

	```
	docpad install ghpages
	```

2. Deploy to GitHub Pages using the plugin

	```
	docpad deploy-ghpages --env static
	```

3. If you'd like deployment automatically to GitHub Pages every time your repo updates, check out the [Continuous Deployment Guide](https://docpad.org/docs/deploy#using-circle-ci-to-deploy-to-github-pages)


### For deployment to a Cloud Data Storage Provider (AWS S3, Google Storage, etc.)

1. [Checkout the DocPad Sunny Plugin](https://github.com/bobobo1618/docpad-plugin-sunny)




## To a Node.js Hosting Provider


### For deployment to [Heroku](http://www.heroku.com)

1. Create a `Procfile` file inside your project that contains:

	```
	web: node_modules/.bin/docpad-server
	```

1. Set your heroku instance to run in production mode

	```
	heroku config:add NODE_ENV=production
	```

1. [Follow the rest of the Heroku guide here](http://devcenter.heroku.com/articles/node-js)

1. If you're also wanting to use custom domains for your website, [follow the Heroku Guide here](https://devcenter.heroku.com/articles/custom-domains), or alternatively here is a generic guide:
	
	1. Login to your domain's DNS manager
	
	1. Create an CNAME Record for your domain pointing to your app url (e.g., `balupton.herokuapp.com`)




### For deployment to [OpenShift](https://openshift.redhat.com)

1. Create your [OpenShift](https://openshift.redhat.com) account and [install their client tools](https://developers.openshift.com/en/managing-client-tools.html)

1. Create a new OpenShift application for your project:

	``` shell
	rhc app create PROJECTNAME https://raw.githubusercontent.com/kyrylkov/openshift-iojs/master/metadata/manifest.yml
	```

1. Set environment variables using:
	
	``` shell
	rhc set-env -a PROJECTNAME NODE_ENV='production'
	```

1. If you'd like a custom domain, run:
	
	``` shell
	rhc alias-add PROJECTWEBSITE.COM -a PROJECTNAME
	```
	
	Then create CNAME record with your DNS host pointing `PROJECTWEBSITE.COM` to `PROJECTNAME-YOUR_OPENSHIFT_NAMESPACE.rhcloud.com`
	
	If you don't know what your OpenShift namespace is, run:
	
	``` shell
	rhc app show -a PROJECTNAME
	```
	
	And it will be listed within the SSH URL.

1. Deploy your project's code to openshift:
	
	``` shell
	rhc app deploy https://github.com/USER/REPO.git#master -a PROJECTNAME
	```

1. You should be all good now! Check the logs of your app with:
	
	``` shell
	rhc tail -a PROJECTNAME
	```


### For deployment to [AppFog](https://www.appfog.com)

1. Create a `app.js` file inside your project that contains:

	``` javascript
	module.exports = require(__dirname+'/node_modules/docpad/out/bin/docpad-server');
	```

1. [Follow the rest of the AppFog guide here](https://docs.appfog.com/getting-started)



### For deployment to [Windows Azure](http://azure.microsoft.com/en-us/services/app-service/web/)

1. Create a deployment script that triggers the static content generation. To create the script run the following command using the [Windows Azure Cross-Platform Command-Line Interface](http://azure.microsoft.com/en-us/documentation/articles/xplat-cli/):

	```
	azure site deploymentscript --basic -t bash
	```

1. Modify the `deploy.sh` file by changing the `# Deployment` section to the following lines. You can see a complete example of the deploy.sh file [here](https://gist.github.com/ntotten/4715760#file-deploy-sh).

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
	./node_modules/.bin/docpad generate
	exitWithMessageOnError "DocPad generation failed"

	# 3. KuduSync
	echo Kudu Sync from "$DEPLOYMENT_SOURCE/out" to "$DEPLOYMENT_TARGET"
	$KUDU_SYNC_COMMAND -q -f "$DEPLOYMENT_SOURCE/out" -t "$DEPLOYMENT_TARGET" -n "$NEXT_MANIFEST_PATH" -p "$PREVIOUS_MANIFEST_PATH" -i ".git;.deployment;deploy.sh" 2> /dev/null
	exitWithMessageOnError "Kudu Sync failed"
	```

1. Last, create a `web.config` file in the `static` directory of your site with the URL rewrite rules shown below. These rules remove the HTML extensions from your URLs. You can see the main portions of this `web.config` file below. You can download the complete file [here](https://gist.github.com/ntotten/4715760#file-web-config).

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



### For deployment to [Modulus](http://modulus.io)

1. [Follow getting started guide](http://help.modulus.io/customer/portal/articles/1640060-getting-started-guide)


### For deployment to [Docker](https://www.docker.io/)

1. [There is a docker file that should help with deployments.](https://github.com/docpad/dockerfile)





## Continuous Deployment

### To GitHub Pages

1. Inside your project directory, do the following:

	1. Add the [GitHub Pages Plugin](/plugin/ghpages) as a Development Dependency

		```
		npm install --save-dev docpad-plugin-ghpages
		```

	1. Add a deploy script to your `package.json` `"scripts"` section:

		``` json
		{
			"scripts": {
				"deploy": "node_modules/.bin/docpad deploy-ghpages --silent --env static"
			}
		}
		```

	1. Remove the `regenerateEvery` property from your DocPad Configuration File if you have set it, as it will no longer be needed.


#### Using Travis CI

1. Inside your GitHub account, do the following:

	1. [Create a Personal Access Token](https://github.com/settings/tokens/new) callled `Travis CI Deployer` that has `repo` and `public_repo` checked (uncheck everything else), make note of the token we'll use it later

1. Inside your project directory, do the following:

	1. Add a `.travis.yml` file to your project with the marked modifications:
		
		``` yaml
		# August 24, 2015
		# https://docpad.org/docs/deploy
		
		# Use the latest travis infrastructure
		sudo: false
		
		# We use node
		language: node_js
		node_js:
		 	- iojs
		cache:
			directories:
				- node_modules
		
		# Prepare and run our tests
		script: "npm test"
		
		# Custom deployment
		after_success: >
			if ([ "$TRAVIS_BRANCH" == "master" ] || [ ! -z "$TRAVIS_TAG" ]) &&
				[ "$TRAVIS_PULL_REQUEST" == "false" ]; then
				echo "Deploying"
				git config --global user.email "travisci@bevry.me"  # substitute with your preference
				git config --global user.name "Bevry Travis CI Deployer"  # substitute with your preference
				git remote rm origin && git remote add origin "https://$GITHUB_AUTH@github.com/docpad/website.git"
				npm run-script deploy
				echo "Deployed"
			else
				echo "Skipped deploy"
			fi
		```
	
	1. Run `travis encrypt "YOUR_GITHUB_USERNAME:THE_PERSONAL_ACCESS_TOKEN" --add env.global`, substitute `YOUR_GITHUB_USERNAME` and `THE_PERSONAL_ACCESS_TOKEN` with the appropriate values


1. All done, your next push to master will be automatically deployed.


#### Using Circle CI

1. Inside your project directory, do the following:

	1. Add a `circle.yml` file to your project with the marked modifications:

		``` yaml
		# August 24, 2015
		# https://docpad.org/docs/deploy
		
		machine:
			node:
				version: "0.12"
		general:
			branches:
				ignore:
				- gh-pages
		dependencies:
			cache_directories:
				- "node_modules"
		machine:
			pre:
				- git config --global user.email "circleci@bevry.me"  # set to your choosing
				- git config --global user.name "Bevry Circle CI Deployer"  # set to your choosing
		deployment:
			production:
				branch: master
				owner: docpad  # set this to the github organisation/profile the owns the repository
				commands:
					- npm run-script deploy
		```

1. Create a SSH Key that will be used by Circle CI to deploy to GitHub Pages, do this by:

	1. Create the SSH Key, make note of where it goes, don't bother with a password, use the email that was inside your `circle.yml` file:

		``` bash
		ssh-keygen -t rsa -b 4096 -C "circle@bevry.me"
		```

	1. Make note of it's location. Two files will be generated. One with `.pub` at the end, which is the public key, and one without `.pub` which is the private key.

1. Inside your Circle CI account, do the following:

	1. Add any environment variables you may need via `Project Settings -> Tweaks -> Environment Variables`

	1. Add the private key to CircleCI via `Project Settings -> Permissions -> SSH Permissions`. Set the hostname to `github.com`. Use the contents of the private key file for the private key text area.

1. Inside your GitHub Project Settings, do the following:

	1. Add the public key to your GitHub Project by going to `Settings -> Deploy Keys -> Add deploy key`. Specify the title as `CircleCI Deployment` or whatever you like and set the key text area to the contents of the public key. Allow write access.

1. If you want to regenerate your website when an external GitHub Repository changes (for instance updating the DocPad Website when the DocPad Documentation repository changes), you will need to:

	1. Create yourself a Circle CI token via the [Circle CI Account API Page](https://circleci.com/account/api)

	1. Go to the settings of the GitHub Repository that should cause the regeneration, and access `Webhooks & Services -> Add webhook`

		1. Specify the `Payload URL` to be:

			```
			https://circleci.com/api/v1/project/YOUR_GITHUB_ORG/YOUR_GITHUB_REPO/tree/master?circle-token=THE_CIRCLECI_TOKEN
			```

		1. Specify `Content type` to be `application/json`, select `Just the push event`, and check `Active`

		1. You can hit that Payload URL whenever you want to retest and rebuild your project.

1. All done, your next push to master will be automatically deployed.

	1. You can now delete the local SSH key files that were made, as they serve no further purpose.
