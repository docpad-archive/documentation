This page serves as a roadmap that details the approximate milestones of DocPad's future.

If this is your first read of this document, you'll probably want to read it starting at the bottom and working your way up. That way you'll be reading things in their planned released order. Instead of big picture to small picture.

Version structure and timelines:

- Version structure is Major.Minor.Patch
- Major.Minor releases are estimated to take 2-4 weeks to complete
- Major releases are estimated to take 4-8 weeks to complete
- Features may not be developed in order - remember this is only a guideline


## Unscheduled

- Authentication Plugin
	- Uses GitHub for authentication, validates email address against `package.json` maintainers
	- Login window trigger by `ctrl/cmd+shift+l`

- REST Plugin

- Web GUI
	- Editing
		- Support adding and removing of resources
		- Support adding and removing of documents
		- Support adding and removing of files (includes uploading if in the cloud)
	- Connect
		- Purchasable Content (e.g. sell premium plugins, tutorials, themes, etc)
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
	- QuickStart
		- Importing content from an existing source (e.g. wordpress, tumblr, jekyll, etc)
	- Connect
		- News
		- Blog
		- Polls
		- Stats
	- QuickStart
		1. Selecting your skeleton
		2. Selecting your plugins
		3. Configuring docpad and plugins
	- Administration
		- Enable/Disable Plugins
		- Configure Plugins and Core


## Current Focus

- [Importer Plugins](https://github.com/bevry/docpad/issues?labels=affects+importer)
	- [WordPress](https://github.com/bevry/docpad/issues/49)
	- [Dropbox](https://github.com/bevry/docpad/issues/386)
	- [Youtube](https://github.com/bevry/docpad/issues/571)
	- [Tumblr](/plugin/tumblr) _**- released**_
	- [Tags](/plugin/tags) _**- released**_
- [Importer Speed Optimisations](https://github.com/bevry/docpad/issues/590)
- [More prominance to Providers/Partners](https://github.com/bevry/docpad-website/issues/19)
- [Web GUI](https://github.com/docpad/gui/issues)
- [Performance optimisations](https://github.com/bevry/docpad/issues/529)
- [Run DocPad on the Client Side](https://github.com/bevry/docpad/issues/542)
- [Official DocPad Blog](https://github.com/bevry/docpad-website/issues/29)
- [Fix Watchr once and for all](https://github.com/bevry/watchr/issues/33)


## Version 6

### v6.46 _**- released**_
- Importer support

### v6.45 _**- released**_
- Added `docpad update` command

### v6.44 _**- released**_
- Virtual document support

### v6.43 _**- released**_
- Added `docpad install` command

### v6.41 _**- released**_
- Debugging and tracing improvements

### v6.38 _**- released**_
- Init empty directories

### v6.35 _**- released**_
- Plugin priorities

### v6.32 _**- released**_
- Streams based logging

### v6.31 _**- released**_
- Progress bar for generation

### v6.30 _**- released**_
- Abstracting out the core begins

### v6.26 _**- released**_
- Node 0.10 support

### v6.25 _**- released**_
- Persistant database

### v6.24 _**- released**_
- Plugins can now extend the CLI

### v6.23 _**- released**_
- Foreign encoding support

### v6.13 _**- released**_
- Statistics

### v6.8 _**- released**_
- `.env` file support

### v6.7 _**- released**_
- [Express.js](http://expressjs.com/) v3 support

### v6.6 _**- released**_
- Added `docpad-debug` executable

### v6.4 _**- released**_
- Custom error pages

### v6.3 _**- released**_
- Multiple environment support

### v6.2 _**- released**_
- Environment specific configuration
- Better node.js deployments
- Better extendability

### v6.1 _**- released**_
- [Element based renderers](https://github.com/bevry/docpad/issues/194)

### v6.0 _**- released**_
- Added differential rendering
- Allow configuration files to hook into events
- Streamlined and cleaned
- Extensible CLI

## Version 5

### v5.2 _**- released**_
- Everything is now parsed into the in-memory database
- Added `docpad.cson` configuration
- Added custom collections via configuration support

### v5.1 _**- released**_
- Added support for binary files

### v5.0 _**- released**_
- Plugins are now handled via NPM
- Uses Backbone for Models and Collections
- Differential replace of the `out` directory


## Version 4

### v4.1 _**- released**_
- Added skeleton exchange

### v4.0 _**- released**_
- Differential replace of the `out` directory


## Version 3

### v3.2 _**- released**_
- You can now select which skeleton on creation of a new project
- Unit Tests
- Modular API for rendering single files
- Modular API for rendering single content blocks
- Hidden files are now ignored in watchr

### v3.1 **- released**
- Added an interactive CLI

### v3.0 **- released**
- New event system, which supports blocking and queuing of events


## Version 2

Version 2 focused on improving the possibilities of the plugin infrastructure as well as adding support for windows and cloud based services.


### v2.3 **- released**
- Cloud Support

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
