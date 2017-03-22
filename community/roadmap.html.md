This page serves as a roadmap what DocPad has done and plans to do.

[You can find out what we have planned over at our Trello.](/trello)

[Want to help? Check out our Contribute Guide.](https://docpad.org/docs/contribute)


## Done

### Version 6

- v6.60
	- Added caching HTTP headers

- v6.59
	- [Fix Watchr once and for all](https://github.com/bevry/watchr/issues/33)

- v6.58
	- Dynamic documents are rendered through the generate action

- v6.56
	- Database caching disabled by default

- v6.55
	- Database caching aka [Importer Speed Optimisations](https://github.com/bevry/docpad/issues/590)

- v6.54
	- Abstracted out notifications into plugin
	- i18n support without native binary

- v6.53
	- Locales can now be merged together

- v6.51
	- Run the local DocPad installation if it exists

- v6.49
	- Cleanup on destroy

- v6.48
	- Version conflict warning

- v6.47
	- Inline elements in styles block

- v6.46
	- [Importer support](https://github.com/bevry/watchr/issues/500)

- v6.45
	- Added `docpad update` command

- v6.44
	- Virtual document support

- v6.43
	- Added `docpad install` command

- v6.41
	- Debugging and tracing improvements

- v6.38
	- Init empty directories

- v6.35
	- Plugin priorities

- v6.32
	- Streams based logging

- v6.31
	- Progress bar for generation

- v6.30
	- Abstracting out the core begins

- v6.26
	- Node 0.10 support

- v6.25
	- Persistant database

- v6.24
	- Plugins can now extend the CLI

- v6.23
	- Foreign encoding support

- v6.13
	- Statistics

- v6.8
	- `.env` file support

- v6.7
	- [Express.js](http://expressjs.com/) v3 support

- v6.6
	- Added `docpad-debug` executable

- v6.4
	- Custom error pages

- v6.3
	- Multiple environment support

- v6.2
	- Environment specific configuration
	- Better Node.js deployments
	- Better extendability

- v6.1
	- [Element based renderers](https://github.com/bevry/docpad/issues/194)

- v6.0
	- Added differential rendering
	- Allow configuration files to hook into events
	- Streamlined and cleaned
	- Extensible CLI

### Version 5

- v5.2
	- Everything is now parsed into the in-memory database
	- Added `docpad.cson` configuration
	- Added custom collections via configuration support

- v5.1
	- Added support for binary files

- v5.0
	- Plugins are now handled via NPM
	- Uses Backbone for Models and Collections


### Version 4

- v4.1
	- Added skeleton exchange

- v4.0
	- Added support for partials


### Version 3

- v3.2
	- You can now select which skeleton on creation of a new project
	- Unit Tests
	- Modular API for rendering single files
	- Modular API for rendering single content blocks
	- Hidden files are now ignored in watchr

- v3.1
	- Added an interactive CLI

- v3.0
	- New event system, which supports blocking and queuing of events


### Version 2

Version 2 focused on improving the possibilities of the plugin infrastructure as well as adding support for windows and cloud based services.


- v2.3
	- Cloud Support

- v2.2
	- Windows Support

- v2.1
	- Dynamic Documents
		- These are rendered per request, and have access to the Express.js request object
		- They enable things like form handling, search, real-time updating data, etc.

- v2.0
	- Plugin's have their own `package.json`
		- This specifies the plugin's dependencies
		- When the plugin is used, DocPad will do a `cd $pluginDir; npm install`
	- Plugins and DocPad configurable through project's `package.json`
	- Plugins and DocPad configurable through project's `docpad.coffee`
	- Front-End Administration Plugin
		- Adds in some client-side JavaScript
		- Utilises contentEditable with semantic properties to update
	- REST Plugin
		- Support read and write of files
		- Requires some sort of authentication method... to be decided

### Version 1

Version 1 focused on improving the scalability, stability, and ease-of-use of DocPad. Bringing it to a vastly superior alternative to other static site generators.

### Version 0

Version 0 focused on fixing the content creation and website development pain.
