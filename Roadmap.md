This page serves as a roadmap that details the approximate milestones of DocPad's future.

For released versions, refer to the "History" section of https://github.com/balupton/docpad


## Upcoming


### v2.2

- Mission Control + QuickStart
  - Used to provide a more intuitive and powerful interface than the CLI
  - QuickStart
    - Provides a web interface for
       1. Selecting your skeleton
       2. Selecting your plugins
       3. Configuring docpad and plugins
  - Mission Control
    - News, Blog, Polls, Stats, Resources (tutorials, screencasts, etc), Plugin Repository etc
    - Plugin + Config administration


### v2.1

- Administration Plugin
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
