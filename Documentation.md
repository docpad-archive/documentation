# DocPad's documentation

Introduction text : what is Docpad, and goal of this documentation.

Important : explain all the technologies that DocPad uses - Node, all the dependencies.

## Core concepts and features

- Generation done from the `src` directory to the `out` directory. (Link to the proper section)
- Manipulation is from the command-line (Link to CLI commands section)
- Generation process is relative to files extensions.
- Nestable layouts
- Access to a database of all documents (Link to the QueryEngine section or the section explaining how to use `@database` and `@collections`)
- Plugins system (Link to the "existing plugins" section or to the plugin development section)

## Installation

References the existing wiki pages or shows their content here ? I'm in favor of showing the content here, like :

### Installing node (and npm)

Official / recommended installation

### Installing docpad

Basically : `npm install docpad` and `docpad install`. Maybe the plugin activation in package.json.

## Basic usage

The existing [Getting Started](https://github.com/bevry/docpad/wiki/Getting-Started) page provides a good base regarding files structure and commands to issue. Needs a bit more explanations though.

## DocPad's CLI

Explain the available commands.

## Getting started with website.docpad

This section could be step-by-step guide to using DocPad. Could be a whole section of its own, maybe hosted in the [website.docpad](https://github.com/bevry/website.docpad) wiki itself. Not sure where it should go, but a basic step-by-step guide would be useful very useful for the "not-so-technical" people.

## Skeletons

They're prompted upon first run, so here we explain what they are.

### Description of the available skeletons

The [Skeletons wiki page](https://github.com/bevry/docpad/wiki/Skeletons) contains good content.

However I'm not sure to understand the difference between a skeleton and a theme.

### How to write a skeleton ?

Explain... how to write a skeleton.

## Files structure

### The `documents` directory

- Contains the content to render based on extensions, like index.html.jade.
- Explain the choice of templating languages
- Path under the `documents` directory will match the final path / url, so each HTML document is a page.
- Explain the true power of DocPad : .htaccess.eco, styles.css.less.coffee or app.js.eco. Yes we can.

### The `public` directory

- Static files copied as is in the out directory. Useful for media assets, javascript libraries, stylesheet.

### The `layout` directory

- Explain the layout system, and the ability of nesting them.
_ Explain how to manipulate content in a layout.

## Data models

This section should detail what are the variables one can use and manipulate

Files are [Backbone models](https://github.com/bevry/docpad/blob/master/src/models/file.coffee)
Documents extend [Backbone models](https://github.com/bevry/docpad/blob/master/src/models/document.coffee)
Every file under the `src` directory is a `File` (Anchor), apart from files under the `documents` directory that are `Document` (Anchor)

### The `File` Class

- Explains the metadata system
- Explains helpers

### The `Document` Class

- Explains the custom metadata system.
- Explains the `toJSON()` method (difference between a `document` and `documentModel`)
- Explains helpers

### `TemplateData`

- Explain what is `TemplateData` : context passed into the template files, accessible with the `this` keyword
- Explain what variables it holds
  - Those from the [DocPad Class](https://github.com/bevry/docpad/blob/master/src/docpad.coffee#L981)
  - Those from the [File Class](https://github.com/bevry/docpad/blob/master/src/models/file.coffee#L36)
  - Those from the [Document Class](https://github.com/bevry/docpad/blob/master/src/models/document.coffee#L32)

This may also need some precisions about what variables are available and when during the rendering process.

## Custom site configuration

Explain here what is the `docpad.cson` file, and how to use it.

## Theme system

This section should explain what themes are, how to use them and how to write one.

### What's a theme ?

### How to use existing theme ?

### How to write a theme ?

## Rendering process

- Explain how the rendering process works, especially the order of events. I think the page about [Plugin Events](https://github.com/bevry/docpad/wiki/Plugin-Events) holds valuable information.

## DocPad plugins

Explain what are plugins, and what they're for. Insist on the different types of plugins : rendering plugins, server plugins (soon/existing ?), CLI plugins (soon?). The previous section about the rendering process helps.

### Useful plugins

Show here the most useful plugins, especially the [Partials plugin](https://github.com/bevry/docpad-extras/tree/master/plugins/partials) and the [Text plugin](https://github.com/bevry/docpad-extras/tree/master/plugins/text).

### Using plugins

- Reference the [docpad-extras](https://github.com/bevry/docpad-extras) repository.
- Explain how to install and activate/deactivate a plugin in the package.json file

### Writing plugins

- Developer docs about writing plugins. The [Plugin Events](https://github.com/bevry/docpad/wiki/Plugin-Events) and the [Writing plugins](https://github.com/bevry/docpad/wiki/Writing-a-Plugin) content is useful here, as well as what variables are available and what should be returned.

## Debugging DocPad

Errors may appear, so DocPad provides a detailed log of activity thanks to the `-d {debug-level}` option. Explain here the various debug levels and what they output. They are also options to debug DocPad core or plugins. The [Debugging DocPad](https://github.com/bevry/docpad/wiki/Debugging) contains lots of useful infos.

## Building the site

The final step before pushing the site to production is to build it : aggregate and compress javascript and css files, mainly. This compression reduces files size and is good for site performance (less HTTP requests). Explain here how to do it.

I don't know to how to do with DocPad though. This may need the existing [Buildr](https://github.com/bevry/docpad-extras/tree/master/plugins/buildr) plugin, or the (soon to come ?) [Grunt](https://github.com/bevry/docpad/issues/212) plugin.

## Using DocPad as a node module

DocPad can be used as a node module inside your project. Explain here how to do it. This [issue](https://github.com/bevry/docpad/issues/206) is just about that.

## Contributing to DocPad

Invite people to contribute ! The existing [Contributing](https://github.com/bevry/docpad/wiki/Contributing) page holds useful informations.

Maybe add a section about how to write tests, or how tests are written so people can jump in (I know I would love this section).