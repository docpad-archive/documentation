This page serves as a roadmap that details the approximate milestones of DocPad's future.

If this is your first read of this document, you'll probably want to read it starting at the bottom and working your way up. That way you'll be reading things in their planned released order. Instead of big picture to small picture.

Version structure and timelines:

- Version structure is Major.Minor.Patch
- Major.Minor releases are estimated to take 2-4 weeks to complete
- Major releases are estimated to take 4-8 weeks to complete.


# Upcoming


## Version 4

Version 4 will enter the SaaS market, allowing people to create their website entirely in the cloud.


## Version 3

Version 3 focuses on connecting the community.

### v3.1

- Web GUI
	- Connect
		- Purchasable Content

### v3.0

- Web GUI
	- Connect
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

### v2.x

- Front-End Administration Plugin
	- Support adding and removing of resources
	- Support adding and removing of documents
	- Support adding and removing of files (includes uploading if in the cloud)


### v2.4

- Web GUI
	- News Centre
		- News
		- Blog
		- Polls
		- Stats


### v2.3

- Web GUI
	- QuickStart
		4. Importing content from an existing source (e.g. wordpress, tumblr, jekyll, etc)


### v2.2

- Web GUI
	- QuickStart
		Provides a web interface for
		1. Selecting your skeleton
		2. Selecting your plugins
		3. Configuring docpad and plugins
	- Administration
		- Enable/Disable Plugins
		- Configure Plugins and Core


### v2.1

- Front-End Administration Plugin
	- Uses GitHub for authentication, validates email address against `package.json` maintainers
	- Adds in some client-side javascript
	- Login window trigger by `ctrl/cmd+shift+l`
	- Utilises contentEditable with semantic properties to update **- done**
- REST Plugin
	- Support read and write of files **- done**
	- Requires some sort of authentication method... to be decided


### v2.0

- Plugin's have their own `package.json`
	- This specifies the plugin's dependencies
	- When the plugin is used, docpad will do a `cd $pluginDir; npm install`
- Plugins and DocPad configurable through project's `package.json`
- Plugins and DocPad configurable through project's `docpad.coffee`


# Released

## Version 1

Version 1 focused on improving the scalability, stability, and ease-of-use of docpad. Bringing it to a vastly superior alternative to other static site generators.

## Version 0

Version 0 focused on fixing the content creation and website development pain.