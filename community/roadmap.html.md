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

- c9.io Support
	- Plugins as npm packages (actually published)
	- c9.io detection in the quickstart to provide alternative instructions
	- use npm module instead of spawn (nice to have)

- Front-End Administration Plugin
	- Support adding and removing of resources
	- Support adding and removing of documents
	- Support adding and removing of files (includes uploading if in the cloud)

- Web GUI
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
		4. Importing content from an existing source (e.g. wordpress, tumblr, jekyll, etc)
	- Connect
		- News
		- Blog
		- Polls
		- Stats
	- QuickStart
		Provides a web interface for
		1. Selecting your skeleton
		2. Selecting your plugins
		3. Configuring docpad and plugins
	- Administration
		- Enable/Disable Plugins
		- Configure Plugins and Core

- Importers
	- WordPress
	- Tumblr
	- Jekyll
	- Octopress

- Deployers
	- Heroku
	- GitHub Pages


## Next

- DocPad Website
- Improved Documentation
- More skeletons
- Importers
- Deployers


## Version 6

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