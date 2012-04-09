- plugins will be moved out of the docpad repo and into the npm registry

	- this will require a naming convention for plugins

		- `docpad-plugin-admin` makes the most sense as all the docpad related stuff will be grouped together in any npm lists (alpha sorting)

	- they must be published with the `package.json` keyword `docpad-plugin`

		- this is so we can find all the plugins when querying the npm registry

	- a possible workflow would be like this:

		- installing docpad:

			1. `npm install docpad`

			2. docpad is installed, and has no knowledge of any plugins yet

			3. some default plugins are listed inside docpad's `package.json` `devDependencies` properties

			4. default plugins can be installed via `docpad install`

			5. the point of the default plugins is so people can still create new websites while offline


		- working with an existing website

			1. `docpad plugin install admin`

			2. this will install the `admin` plugin to the website's `node_modules`

			3. as well as add the plugin to the website's `package.json` `dependencies` property

			4. this makes it so that on deployment, your website has all the plugins it needs installed via it's `package.json`, and `docpad` does not need to install anything


		- whenever a plugin is installed

			1. docpad will also install it into docpad's `node_modules` so that it can cache it

			2. docpad will update a global config file (e.g. `~/.docpad.config.json`) with the list of all cached plugins, so that when docpad is re-installed we can read the cache file and re-install all cached plugins



- skeletons will be moved from git repos into the npm registry

	- they must be published with the `package.json` keyword `docpad-skeleton`

		- this is so we can find all the skeletons when querying the npm registry

	- problems

		- they will no longer have their git references, meaning that no git history, etc, making it harder to submit pull requests etc






