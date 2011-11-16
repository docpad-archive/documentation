This page serves as a roadmap that details the approximate milestones of DocPad's future.

If this is your first read of this document, you'll probably want to read it starting at the bottom and working your way up. That way you'll be reading things in their planned released order. Instead of big picture to small picture.

Version structure and timelines:

- Version structure is Major.Minor.Patch
- Major.Minor releases are estimated to take 2-4 weeks to complete
- Major releases are estimated to take 4-8 weeks to complete
- Features may not be developed in order - remember this is only a guideline


## Unscheduled

- Asynchronous documents
	- Could specify `async: true` in the meta data, and call `@next(err)` for completion

- Authentication Plugin
	- Uses GitHub for authentication, validates email address against `package.json` maintainers
	- Login window trigger by `ctrl/cmd+shift+l`


## Version 4

Version 4 enters the SaaS market, allowing people to create their website entirely in the cloud.

### v4.0

- Front-End Administration Plugin
	- Support adding and removing of resources
	- Support adding and removing of documents
	- Support adding and removing of files (includes uploading if in the cloud)


## Version 3

Version 3 focuses on connecting the community.

### v3.1

- Web GUI
	- Connect
		- Purchasable Content (e.g. sell premium plugins, tutorials, themes, etc)

### v3.0

- Web GUI
	- Exchange
		- Community Centre
			- Chat
			- Discussion Boards
			- ShowCase
		- Extension Centre
			- Skeletons
			- Plugins
			- Rate and Discuss
		- Learning Centre (tutorials, videos, etc)


## Version 2

Version 2 focuses on ease of use. This is done with the addition of front-end administration, and the introduction of a web interface for installing and configuring your docpad instance.


### v2.5

- Web GUI
	- QuickStart
		4. Importing content from an existing source (e.g. wordpress, tumblr, jekyll, etc)


### v2.4

- Web GUI
	- Connect
		- News
		- Blog
		- Polls
		- Stats


### v2.3

- Web GUI
	- QuickStart
		Provides a web interface for
		1. Selecting your skeleton
		2. Selecting your plugins
		3. Configuring docpad and plugins
	- Administration
		- Enable/Disable Plugins
		- Configure Plugins and Core


### v2.2 **- released**

- Windows Support


### v2.1 **- released**

- Dynamic Documents
	- These are rendered per request, and have access to the express.js request object
	- They enable things like form handling, search, real-time updating data, etc.


### v2.0 **- released**

- Plugin's have their own `package.json`
	- This specifies the plugin's dependencies
	- When the plugin is used, docpad will do a `cd $pluginDir; npm install`
- Plugins and DocPad configurable through project's `package.json`
- Plugins and DocPad configurable through project's `docpad.coffee`
- Front-End Administration Plugin
	- Adds in some client-side javascript
	- Utilises contentEditable with semantic properties to update
- REST Plugin
	- Support read and write of files
	- Requires some sort of authentication method... to be decided



## Version 1 **- released**

Version 1 focused on improving the scalability, stability, and ease-of-use of docpad. Bringing it to a vastly superior alternative to other static site generators.

## Version 0 **- released**

Version 0 focused on fixing the content creation and website development pain.